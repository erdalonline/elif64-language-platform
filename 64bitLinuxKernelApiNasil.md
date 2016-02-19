## x86\_64 Mimarisinde Linux Kernel API Çağrıları Nasıl Gerçekleştirilir ##
  1. RAX yazmacı(register) sistem çağrı numarasını belirtir (60: sys\_exit gibi...)
  1. Parametreler sırası ile RDI, RSI, RDX, [R10](https://code.google.com/p/elif64-language-platform/source/detail?r=10), [R8](https://code.google.com/p/elif64-language-platform/source/detail?r=8), [R9](https://code.google.com/p/elif64-language-platform/source/detail?r=9) yazmaçlarına kaydedilir. (Sistem çağrısı ne kadarına ihtiyaç duyuyorsa o kadarı kullanılır)
  1. Sistem çağrısı sonrasında RCX ve [R11](https://code.google.com/p/elif64-language-platform/source/detail?r=11) yazmaçlarının içeriği değişir.
  1. Sistem çağrısı, geri dönüş değeri için RAX ve RDX yazmaçlarını kullanır. (RDX'e çoğu zaman ihtiyaç duyulmaz)
  1. [[-4095,-1]] kapalı aralığındaki dönüş değerleri hata belirtir. Değer -1 ile çarpılarak hata kodu(errno) elde edilebilir.
  1. RCX, [R11](https://code.google.com/p/elif64-language-platform/source/detail?r=11) ve geri dönüş yazmaçları dışındaki yazmaçların içerikleri korunur.
  1. 32-bit Linux API çağrıları "int 0x80" komutu ile gerçekleştiriliyordu. 64-bit Linux API çağrılarında "syscall" komutu kullanılır.
  1. 32-bit sistem çağrı numaraları ile 64-bit sistem çağrı numaraları birbirinden farklıdır.
  1. 32-bit sistem çağrı örnekleri 64-bit Linux'larda aynen çalışır fakat gerçek 64-bit kipinde çalışmak istiyorsanız syscall yöntemini kullanmalısınız.



## Örnek Uygulama ##

Aşağıdaki örnek kod 64-bit Linux için iki adet sistem çağrısını içerir.<br>
İlk syscall komutu ekrana "Merhaba Dünya!" metnini basar. İkinci çağrı ise uygulamayı sonlandırır.<br>
<hr />
<pre><code>bits 64<br>
<br>
global _start<br>
<br>
section .data<br>
	hello:		db 'Merhaba Dünya!',10<br>
<br>
section .text<br>
<br>
_start:<br>
<br>
	mov rdx,16		; length of string<br>
	mov rsi,hello		; string offset<br>
	mov rdi,1		; file descriptor : 1 - standard output<br>
	mov rax,1		; system call : sys_write<br>
	syscall			; Call the kernel<br>
<br>
	xor rdi,rdi		; exit status : 0<br>
	mov rax,60		; system call : sys_exit<br>
	syscall			; Call the kernel<br>
<br>
</code></pre>
<hr />
Kaynak kodu "p08.asm" ismi ile kaydettikten sonra aşağıdaki gibi nasm ile derleyip ld ile çalıştırılabilir dosya haline getirebilirsiniz.<br>
<pre><code>nasm -f elf64 -l p08.list p08.asm<br>
ld -s -o p08 p08.o<br>
./p08<br>
Merhaba Dünya!<br>
</code></pre>
Uygulamamız 536 byte'dır. İstenirse daha da küçültülebilir.<br>
<pre><code>engin@x:~$ ls -l p08<br>
-rwxr-xr-x 1 engin engin 536 2011-03-27 20:20 p08<br>
</code></pre>
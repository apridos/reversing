# Apa itu Software Reverse Engineering?

Merupakan proses analisis terhadap sebuah software yang kita tidak miliki _source code_-nya. 
Analisis yang kita lakukan bertujuan untuk mengekstraksi informasi demi mengetahui bagaimana _software_ tersebut bekerja atau bahkan menemukan bug. 
Proses ini dilakukan dengan mengamati perilaku _software_ pada abstraksi paling rendah, yaitu _machine code_.

Kita juga mengetahui bahwa pada umumnya _software_ ditulis pada bahasa tingkat tinggi seperti C, C++, Python dan lainnya. 
Pada akhirnya, kode ini nantinya akan diterjemahkan ke dalam bahasa mesin (_machine code_) – serangkaian _bytes_ yang dimengerti oleh CPU. 
Proses mengkonstruksi kembali _machine code_ ke dalam bahasa Assembly disebut dengan _disassembly_.

## Proses Compiling pada Program C

Berikut ini adalah program hello.c:

```
#include<stdio.h>

int main(){
        printf("Hello!");
        return 0;
}
```

### **_Preprocessing_**

Pada tahap ini, semua komentar pada kode akan dibuang. 
Semua *macro* akan digantikan dengan nilai yang sebenarnya dan juga berkas dari _header_ yang berekstensi **.h** akan ditambahkan. 
Sederhananya, *preprocessor* adalah :

> is just a text substitution tool and it instructs the compiler to do required pre-processing before the actual compilation
> 
> _https://www.tutorialspoint.com/cprogramming/c_preprocessors.htm_

Berhenti setelah _preprocessing_ selesai :
```
root@coyote:~# gcc -E hello.c
```

### **_Compilation_**

Menggunakan *compiler*, berkas yang sudah melewati tahap _preprocessing_ kemudian dibuatkan _IR (Intermediate Representation) code_-nya. 
Pada akhir proses ini akan diperoleh berkas baru berekstensi **.s** yang sebenarnya berbentuk *assembly code*.

> An intermediate representation is a representation of a program “between” the source and target languages.
> 
> _https://cs.lmu.edu/~ray/notes/ir/_

Berhenti setelah _compilation_ selesai :
```
root@coyote:~# gcc -S hello.c
```
### **_Assembly_**

Asssembler kemudian menerjemahkan _IR code_ ke dalam _object code_ dengan ekstensi berkas **.o** di UNIX atau **.obj** di DOS.

Berhenti setelah _assembly_ selesai :
```
root@coyote:~# gcc -c hello.c
```

### **_Linking_**

Kita tahu pada program yang ditulis dalam bahasa C menggunakan banyak fungsi. 
Fungsi-fungsi ini adalah _pre-compiled_, dan _object code_-nya sudah tersimpan dengan ekstensi **.a** atau **.lib**. 
Fungsi utama dari **linker** adalah mengkombinasikan _object code_ dari fungsi yang sudah ada dengan _object code_ program yang kita tulis. 
Setelah melewati tahap ini, kita akan memperoleh berkas yang _executeable (machine code)_ dengan bentuk _PE (Portable Executable)_ di DOS dan berkas _ELF (Executable and Linkable Format)_ di UNIX.

_Complete compilation_:
```
root@coyote:~# gcc hello.c -o executable
```



> Machine code is binary (1’s and 0’s) code that can be executed directly by the CPU. If you were to open a machine code file in a text editor you would see garbage, including unprintable characters (no, not those unprintable characters 😉 ).
>
> Object code is a portion of machine code that hasn’t yet been linked into a complete program. It’s the machine code for one particular library or module that will make up the completed product. It may also contain placeholders or offsets not found in the machine code of a completed program. The linker will use these placeholders and offsets to connect everything together.
>
> Assembly code is plain-text and (somewhat) human read-able source code that mostly has a direct 1:1 analog with machine instructions. This is accomplished using mnemonics for the actual instructions, registers, or other resources. Examples include JMP and MULT for the CPU’s jump and multiplication instructions. Unlike machine code, the CPU does not understand assembly code. You convert assembly code to machine with the use of an assembler or a compiler, though we usually think of compilers in association with high-level programming language that are abstracted further from the CPU instructions.
>
> _https://stackoverflow.com/questions/466790/assembly-code-vs-machine-code-vs-object-code_


### Referensi

https://medium.com/@laura.derohan/compiling-c-files-with-gcc-step-by-step-8e78318052

https://www.javatpoint.com/compilation-process-in-c

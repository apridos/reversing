# Executable and Linkable Format File

## ELF header

![ELFHeader](/0x02/ELFHeader.png)

Bisa saja berukuran 52 byte atau 64 byte, tergantung dari arsitektur CPU. Di dalamnya terdapat informasi seperti:
_magic_
_class_ yang ketika bernilai 1 berarti arsitekturnya adalah 32-bit dan ketika bernilai 2 arsitekturnya adalah 64-bit.
_endianness_
_version_
_Application Binary Interface_
[_machine_
_file type_ 	: CORE untuk core
		: DYN (shared object file)
		: EXEC (executable)
		: REL]
_entry point_
dll

## PROGRAM HEADER TABLE (Hanya ada di EXEC dan DYN)

![ProgramHeaderTable](/0x02/ProgramHeaderTable.png)

Struktur array yang mendeskripsikan bagaimana nantinya program dipetakan ke dalam _virtual memory_





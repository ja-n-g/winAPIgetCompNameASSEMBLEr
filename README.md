# winAPIgetCompNameASSEMBLEr
.386
.model flat, stdcall
option casemap:none

include windows.inc
include kernel32.inc
include user32.inc
includelib kernel32.lib
includelib user32.lib

.data
    computerName db 256 dup(0)   ; Буфер для хранения имени компьютера
    sizeOfName   dd 256          ; Размер буфера
    msgCaption   db "Computer Name", 0
    msgFormat    db "Computer Name: %s", 0

.code
start:
    ; Вызов GetComputerNameA
    invoke GetComputerNameA, addr computerName, addr sizeOfName
    
    ; Вывод результата через MessageBox
    invoke wsprintfA, addr computerName, addr msgFormat, addr computerName
    invoke MessageBoxA, 0, addr computerName, addr msgCaption, MB_OK
    
    ; Завершение программы
    invoke ExitProcess, 0

end start

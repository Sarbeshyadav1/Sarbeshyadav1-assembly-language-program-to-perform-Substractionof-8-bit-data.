# Sarbeshyadav1-assembly-language-program-to-perform-Substractionof-8-bit-data.
Write a program in assembly language to perform subtraction of 8-bit data.
CODE

org 100h

num1 db 20h
num2 db 10h

start:
    mov al, num1
    sub al, num2
    mov ah, 0
    add al, 30h
    mov dl, al
    mov ah, 02h
    int 21h
    mov ah, 4Ch
    int 21h

end start

output

![image](https://github.com/user-attachments/assets/f1f55c1e-b83a-442c-9612-a9b6bd128f89)


Explanation:
org 100h:

This directive tells the assembler to start the program's code at memory offset 100h. This is standard for COM files in DOS.
num1 db 20h and num2 db 10h:

These lines define two 8-bit data values. num1 is set to 20h (hexadecimal for 32 in decimal) and num2 is set to 10h (hexadecimal for 16 in decimal).
start:

This label marks the beginning of the program's executable code.
mov al, num1:

This instruction moves the value stored in num1 (which is 20h) into the AL register. AL is the lower 8 bits of the AX register.
sub al, num2:

This subtracts the value stored in num2 (which is 10h) from the value currently in AL (which is 20h). The result (10h, or 16 in decimal) is stored back in AL.
mov ah, 0:

This clears the AH register by moving 0 into it. However, in this context, this step is unnecessary because AH is not used in further arithmetic or logic operations.
add al, 30h:

This converts the result in AL from binary to ASCII. Adding 30h (48 in decimal) converts the value in AL to its corresponding ASCII character. For example, if AL contains 10h (16 in decimal), adding 30h makes it 40h, which corresponds to the character '0' when interpreted as an ASCII character.
mov dl, al:

This moves the ASCII value in AL to DL, which is the register used by DOS interrupt 21h to print a character.
mov ah, 02h:

This sets up the AH register with the value 02h, which is the DOS function number for displaying a character on the screen.
int 21h:

This interrupt call triggers the DOS function specified in AH (02h), which outputs the character in DL to the screen. In this case, it displays the ASCII character corresponding to the subtraction result.
mov ah, 4Ch:

This sets up AH with the value 4Ch, which is the DOS function number for terminating the program.
int 21h:

This interrupt call triggers the DOS function specified in AH (4Ch), which terminates the program and returns control to the operating system.
end start:

This directive marks the end of the source code and specifies the entry point for the program (the start label).
Summary:
The code subtracts 10h (16 in decimal) from 20h (32 in decimal), resulting in 10h (16 in decimal).
It then converts the result (10h) to its ASCII equivalent ('0') and prints it on the screen.
The program then terminates.
This program will output the character corresponding to the result of the subtraction (in this case, '0') on the screen when run. If you need the result displayed as a two-digit decimal, additional logic would be required.

2. Write an assembly language program to perform subtraction of 16-bit data.

CODE

org 100h

num1 dw 1234h
num2 dw 5678h

start:
    mov ax, num1
    sub ax, num2
    mov bl, ah
    mov bh, al
    mov ah, bl
    shr ah, 4
    add ah, 30h
    cmp ah, 39h
    jle print_high
    add ah, 7
print_high:
    mov dl, ah
    mov ah, 02h
    int 21h
    mov ah, bh
    and ah, 0Fh
    add ah, 30h
    cmp ah, 39h
    jle print_low
    add ah, 7
print_low:
    mov dl, ah
    mov ah, 02h
    int 21h
    mov ah, 4Ch
    int 21h

end start

output
![image](https://github.com/user-attachments/assets/b3d6d15e-ea29-4cb8-aec8-82549e24d11b)


Explanation:
org 100h:

This directive tells the assembler to start the program's code at memory offset 100h. This is typical for COM files in DOS.
num1 dw 1234h and num2 dw 5678h:

These lines define two 16-bit data values. num1 is set to 1234h (hexadecimal for 4660 in decimal), and num2 is set to 5678h (hexadecimal for 22136 in decimal).
mov ax, num1:

This instruction moves the value stored in num1 (1234h) into the AX register.
sub ax, num2:

This subtracts the value stored in num2 (5678h) from the value currently in AX (1234h). The result is stored back in AX. The result will be AX = 1234h - 5678h = -4444h, which in hexadecimal will result in a large number due to how negative numbers are represented in 16-bit two's complement (in this case, BBBC in hexadecimal).
mov bl, ah and mov bh, al:

The high byte of AX (which is stored in AH) is moved to BL.
The low byte of AX (which is stored in AL) is moved to BH.
mov ah, bl:

This moves the value in BL back into AH.
shr ah, 4:

This instruction shifts the high nibble of AH right by 4 bits, effectively isolating the high nibble.
add ah, 30h:

Converts the high nibble of AH to an ASCII character by adding 30h.
cmp ah, 39h and jle print_high:

Compares AH to 39h. If AH is less than or equal to 39h, it jumps to the print_high label. This is to handle the hexadecimal digits 0-9.
add ah, 7:

This converts any hexadecimal values A-F to their corresponding ASCII values (since they need to be represented as 'A' to 'F').
print_high:

Moves the high nibble of the result into DL and prints it using DOS interrupt 21h function 02h.
mov ah, bh:

Moves the original low byte of AX (which was stored in BH) back into AH.
and ah, 0Fh:

Isolates the low nibble of AH by performing a bitwise AND with 0Fh.
add ah, 30h:

Converts the low nibble of AH to an ASCII character by adding 30h.
cmp ah, 39h and jle print_low:

Compares AH to 39h. If AH is less than or equal to 39h, it jumps to the print_low label. This handles the digits 0-9.
add ah, 7:

Converts any hexadecimal values A-F to their corresponding ASCII values.
print_low:

Moves the low nibble of the result into DL and prints it using DOS interrupt 21h function 02h.
mov ah, 4Ch and int 21h:

Terminates the program by calling DOS interrupt 21h with function 4Ch.
Summary:
The program performs a 16-bit subtraction of two values (1234h and 5678h).
It then converts the high and low nibbles of the result into ASCII characters and prints them.
This program is designed to display the result of a subtraction as a hexadecimal value, not a decimal value.
The subtraction of 1234h and 5678h results in a negative value (BBBC in hexadecimal), and this program will display the hexadecimal result.





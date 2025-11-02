# FIBONACCI SERIES USING 8086 MICROPROCESSOR

## AIM
To write an assembly language program in 8086 to generate the Fibonacci Series up to N terms and store the sequence in memory.

## APPARATUS REQUIRED


1. Personal Computer
2. MASM Software

## PROBLEM ANALYSIS
The first and second term of the Fibonacci series are 00 and 01. The third element is given by the sum of the first and second element. The fourth element is given by sum of second and third element, and so on. In general, an element of fibonacci series is given by sum of immediate two previous element.

## ALGORITHM
1. Set SI-register as pointer for Fibonacci series.
2. Set CL-register as count for number of elements to be generated.
3. Increment the pointer (SI).
4. Initialize the first element of Fibonacci series as 00H in AL-register.
5. Store first element in memory.
6. Increment the pointer (SI).
7. Increment AL to get second element (01H) of Fibonacci series in AL-register.
8. Store the second element in memory.
9. Decrement the count (CL-register) by 02.
10. Decrement the pointer (SI).
11. Get the element prior to last generated element in AL.
12. Get the last generated element in BL.
13. Add the previous two elements (AL and BL) to get the next element in AL.
14. Increment the pointer.
15. Store the next element (AL) of the Fibonacci series in memory.
16. Decrement the count (CL).
17. If the content of CL is not zero then go to step 10, otherwise stop.

## FLOW CHART
<img width="733" height="581" alt="image" src="https://github.com/user-attachments/assets/8748bff2-c5d6-4c7a-93a2-c946e794a8a0" />








## PROGRAM
```asm
DATA SEGMENT
    COUNT DB 10
    SERIES DB 10 DUP(0)
DATA ENDS

CODE SEGMENT
    ASSUME CS:CODE, DS:DATA
START:           
    MOV AX, DATA
    MOV DS, AX
    LEA SI, SERIES
    MOV CL, [COUNT]
    MOV AL, 00H
    MOV [SI], AL
    INC SI
    INC AL
    MOV [SI], AL
    SUB CL, 02H
    JZ  STOP_PROGRAM
LOOP_START:
    DEC SI
    MOV AL, [SI]
    INC SI
    MOV BL, [SI]
    ADD AL, BL
    INC SI
    MOV [SI], AL
    DEC CL
    JNZ LOOP_START
STOP_PROGRAM:
    MOV AH, 4CH
    INT 21H
CODE ENDS
    END START
```






## OUTPUT IMAGE FROM MASM SOFTWARE

<img width="643" height="397" alt="image" src="https://github.com/user-attachments/assets/b4be7f7f-8784-4375-8d5e-c9ccfa68968f" />



<img width="643" height="222" alt="image" src="https://github.com/user-attachments/assets/a2186cb3-f924-41f5-8dc0-a3d04ded28ad" />




<img width="636" height="395" alt="image" src="https://github.com/user-attachments/assets/25564b43-eff1-498e-a494-24fcd2fd8068" />

## RESULT
Thus, the Assembly Language Program for 8086 to generate the Fibonacci Series up to N terms and store the sequence in memory was successfully written and executed using MASM.

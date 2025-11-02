# GENERATION OF 100 MS DELAY USING 8051

## AIM
To write an assembly language program in 8051 to generate a 100 ms delay using Timer 1 in Mode 2 and toggle Port 2.5 continuously.

## APPARATUS REQUIRED

1. Personal Computer
2. Keil Software

## ALGORITHM
1. **Start the program.**
2. **Initialize Timer 1 in Mode 2 (8‑bit auto‑reload) by loading TMOD ← 20H.**
3. **Load TH1 with 00H (reload value for Timer 1).**
4. **Enter the main loop (HERE):**
       - Load register R6 ← 2 (outer loop counter).
5. **Outer loop (OUTER):**
       - Load register R5 ← 196 (inner loop counter).
6. **Inner loop (INNER):**
       - Start Timer 1 (SETB TR1).
       - Wait until Timer 1 overflow flag TF1 is set.
       - Stop Timer 1 (CLR TR1).
       - Clear overflow flag (CLR TF1).
       - Decrement R5. If not zero, repeat inner loop.
7. **After inner loop completes:**
       - Toggle bit P2.5 (complement its value).
       - Decrement R6. If not zero, repeat outer loop.
8. **After outer loop completes:**
       - Jump back to HERE to repeat the entire process continuously.

## PROGRAM
```asm
ORG 0000H
MOV TMOD, #20H
MOV TH1, #00H
HERE:
    MOV R6, #2
OUTER:
    MOV R5, #196
INNER:
    SETB TR1
WAIT:
    JNB TF1, WAIT
    CLR TR1
    CLR TF1
    DJNZ R5, INNER
    CPL P2.5
    DJNZ R6, OUTER
    SJMP HERE
END
```






## OUTPUT IMAGE FROM MASM SOFTWARE

<img width="1918" height="751" alt="image" src="https://github.com/user-attachments/assets/fc670c59-eba4-4781-8e80-2bd861668302" />


## RESULT
Thus, the Assembly Language Program for 8051 to generate a 100 ms delay using Timer 1 in Mode 2 and continuously toggle Port 2.5 was successfully written, assembled, and executed. The output observed was a continuous square wave on pin P2.5 with a time period of approximately 200 ms (100 ms HIGH and 100 ms LOW).

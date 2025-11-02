# GENERATION OF 100 MS DELAY USING 8051

## AIM
To write an assembly language program in 8051 to generate a 100 ms delay using Timer 1 in Mode 2 and toggle Port 2.5 continuously.

## APPARATUS REQUIRED

1. Personal Computer
2. Keil Software

## ALGORITHM
1. **Start the program.**
2. **Initialize Timer:**
   - Load the Timer Mode register (TMOD) with 20H to select Timer 1 in Mode 2 (8‑bit auto‑reload).
   - Load the TH1 register with the required reload value (e.g., 00H in your code, or 9CH in the earlier calculation depending on the delay scheme).
3. **Enter the main loop (HERE):**
   - Load outer loop counter (R6) with a fixed value (e.g., 02H) to control the number of large delay blocks.
4. **Outer loop (OUTER):**
   - Load inner loop counter (R5) with a fixed value (e.g., C4H = 196) to control the number of timer overflows per outer cycle.
5. **Inner loop (INNER):**
   - Start Timer 1 by setting the run control bit TR1.
   - Wait for overflow: Continuously check the overflow flag TF1 until it becomes 1.
   - Stop Timer 1 by clearing TR1.
   - Clear the overflow flag TF1 to prepare for the next cycle.
   - Decrement R5. If R5 ≠ 0, repeat the inner loop.
6. **After inner loop completes:**
   - Toggle Port 2.5 using CPL P2.5 (if it was HIGH, it becomes LOW; if it was LOW, it becomes HIGH).
7. **Decrement outer loop counter (R6):**
   - If R6 ≠ 0, repeat the outer loop.
   - If R6 = 0, reload R6 and restart the process.
8. **After outer loop completes:**
   - Repeat the entire sequence continuously, ensuring Port 2.5 keeps toggling with the required delay.
9. **End.**

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

## OUTPUT

<img width="1918" height="751" alt="image" src="https://github.com/user-attachments/assets/fc670c59-eba4-4781-8e80-2bd861668302" />


## RESULT
Thus, the Assembly Language Program for 8051 to generate a 100 ms delay using Timer 1 in Mode 2 and continuously toggle Port 2.5 was successfully written, assembled, and executed. The output observed was a continuous square wave on pin P2.5 with a time period of approximately 200 ms (100 ms HIGH and 100 ms LOW).

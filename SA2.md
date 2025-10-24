
# Skill Assessment 2

## AIM:
Write an assembly language program in 8051 to generate a 1 second delay using Timer 1 in Mode 1 and toggle all bits of Port 1 continuously.



## APPARATUS REQUIRED:
- Personal Computer  
- Keil Software  

## ALGORITHM

### 1.Initialization:
    Load accumulator A with 0FFH (all bits set to 1).
    Move this value to Port 1 (P1), setting all pins high initially.

### 2.Main Loop (TOGGLE_LOOP):
    Complement (toggle) the bit P1.0 using the CPL instruction on bit 0 of P1.
    Call the subroutine DELAY_1S to generate approximately 1-second delay.
    Jump back to TOGGLE_LOOP to repeat toggling indefinitely.

### 3.DELAY_1S Subroutine:
    Load R2 with 15 as the outer loop counter.
    Inside DELAY_LOOP:
    Set Timer 1 mode to mode 1 (16-bit timer) by loading TMOD with 10H.
    Load TH1 and TL1 with values (BCH and FFH) to preset timer counts for delay.
    Start Timer 1 by setting TR1.
    Wait (poll) until Timer 1 overflow flag TF1 is set.  
    Stop Timer 1 and clear TF1.
    Decrement R2 and if not zero, repeat delay loop for accumulated delay.
    Return from subroutine after delay completes.

### 4.Terminate program with interrupt 21h service to exit.


## PROGRAM:

### Reversing an array:

```
ORG 0000H
MAIN:
    MOV A, #0FFH        
    MOV P1, A            
TOGGLE_LOOP:
    CPL P1.0
    ACALL DELAY_1S
    SJMP TOGGLE_LOOP
DELAY_1S:
    MOV R2, #15
DELAY_LOOP:
    MOV TMOD, #10H
    MOV TH1, #0BCH
    MOV TL1, #0FFH
    SETB TR1
WAIT_OV:
    JNB TF1, WAIT_OV

    CLR TR1
    CLR TF1
    DJNZ R2, DELAY_LOOP
    RET

END MAIN

```
## OUTPUT:

![WhatsApp Image 2025-10-24 at 00 04 59_53bb4502](https://github.com/user-attachments/assets/51db3f62-913e-4efc-9cb8-399cbf58eef9)

## RESULT:
Thus ,The program to to generate a 1 second delay using Timer 1 in Mode 1 and toggle all bits of Port 1 continuously was done and shown the output.

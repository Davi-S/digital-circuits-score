# Report

When a sum input is pressed, an encoder converts the button value into its binary representation. This binary value is then stored in a register that retains the value of the last sum button clicked. Simultaneously, this same value is added to the current content of another register, which stores the total score value. The result of this addition replaces the previous value in the score register.

The encoder responsible for button conversion can encode up to 10 buttons (values from 0 to 9). Only 5 of these inputs are used, as required by the assignment.

The sum buttons and the *undo* button act as the system’s own *clock* signal. When a button is pressed, the register associated with the value is triggered, saving the result. When the button is released, the register is locked, preventing the value 0 from being inadvertently stored.

An RS flip-flop is connected to the buttons and the ALU. This flip-flop is configured so that the addition operation is selected when a sum button is pressed (*set*), and the subtraction operation is selected when the *undo* button is pressed (*reset*). Keeping the ALU operator selected even after the buttons are released is crucial for system stability, preventing the operation result from changing prematurely and, consequently, saving the wrong value in the score memory.

The score register operates inversely to the button register. The score register is released for updating only when no buttons are pressed, and it is locked when a button is pressed. This logic is essential to avoid infinite addition cycles and to ensure correct score updating.

When the *undo* button is pressed, the value stored in the register that holds the last button clicked is subtracted from the current score value. This new resulting value is then saved in the score register. This subtraction action can be performed indefinitely, and the same value (from the last sum button clicked) will always be subtracted.

The score display is implemented using two 7-segment displays. A specific decoder converts the binary value of the score register into appropriate signals to drive these displays.

When the score reaches 50 or more, an LED is triggered, indicating the “end of the game.” This is achieved using a specific comparator.

If the score is subtracted to the point of going below zero, it cyclically returns to 255.

# Volatile
#include "mbed.h"

// Using `volatile` ensures that the value of buttonPressed is always read from memory, preventing the compiler from optimizing it in ways that may cause it to miss changes updated by the ISR.
// Ensure that the ISR does minimal work to avoid issues like race conditions or resource locking that can happen with complex operations inside an ISR.

InterruptIn button(USER_BUTTON);
volatile bool buttonPressed = false;

void onButtonPress() {
    buttonPressed = true;
}

int main() {
    while (true) {
        if (buttonPressed) {
            printf("Button pressed\n");
            buttonPressed = false;
        }
        ThisThread::sleep_for(1000ms); // Sleep to prevent flooding the output with messages.
    }
}

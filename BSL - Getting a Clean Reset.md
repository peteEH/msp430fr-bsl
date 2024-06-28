# BSL - A Clean Reset

**Methods to get code to run 'as if' a POR or RESET_N pin was toggled...**

## Summary

- Jumping directly to loaded code by updating the program counter can get messy if the code gets complex
- Using a simple "Hello World" (Blink) program to demonstrate loader capability
- Loading code into memory from the TI-TXT (TI-TXT Hex Format) generated file and jumping to the start of memory does seem to work, i.e. dropping the code into 0xC400 on a 15KB device and jumping does "blink"
- The reset vector (0xFFFE) contains 0xC438 - jumping the program counter to 0xFFFE does not seem to work, no blinking LED
- I wanted a clean, known reset generated when starting a newly dropped program... I can't always have access to the physical RESET pin when installed/in-circuit

## Solution

- After loading the code into 0xC400 - you can exploit the watchdog timer control register (located at base address of 0x01CC on the MSP430FR2433)
- By not writing the correct WDT password (WDTPW, correct password: 0x5A) into the control register - the chip will issue a Power-up clear (PUC)

## Applicability and Limitations

- Verified to work on the MSP430FR2433 - double check devices that are much different
- The BSL has to be unlocked for this to work - so this is a "after you're done loading code and want to let go of control"
- Once the PUC event kicks the BSL out of control - the main application code will execute and subsequent BSL sessions will require a new unique password to be provided from the code that was loaded
- The BSL password will be discussed in another article

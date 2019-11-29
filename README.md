# CyberLib
Fast library for Arduino from [cyber-place.ru] (http://cyber-place.ru/showthread.php?t=550)

## Pin management:
`` `c ++
Dx_Out; // setting pin X as an output
Dx_In; // setting pin X as input
Dx_Hihg; // setting a high level on pin X
Dx_Low; // setting low on pin X
Ax_Read; // read analog pin X
`` ``
## SmallUart
`` `c ++
UART_Init (115200); // serial port initialization
UART_ReadByte (byte)); // get byte of data from the serial port
UART_SendByte (byte); // send byte of data to the serial port
UART_SendArray (array, size array); // The function sends to the UART port, a byte array, the maximum amount of which should not exceed 65535 bytes, the minimum array size is 1 byte. You can also send part of the array. Array is the name of your array, size array is the number of bytes sent to the array
`` ``
## delay_us () and delay_ms ()
The functions `delay_us ()` and `delay_ms ()` can be used in interrupts, since they do not use a timer, but we should not forget that the accuracy of these functions depends on the use of interrupt handlers in the code. If you do not use interrupts in the code, then the accuracy will be high
`` `c ++
delay_us (n); // where n is the delay in microseconds, the maximum delay can be no more than 16000 microseconds
delay_ms (n); // where n is the delay in ms, the maximum delay can be no more than 65000 ms, this is 65 seconds
`` ``
## Timer1
The timer interrupt setting can be configured from 6 μs to 4,000,000 μs (4 seconds) in 1 μs increments.
`` `c ++
StartTimer1 (handler, 1000); // start the timer, the first parameter is your interrupt handler, the second parameter is the time, it can take values ​​from 6 to 4000000
StopTimer1 (); // Turn off the timer
ResumeTimer1 (); // resume countdown after stopping
RestartTimer1 (); // restart the timer countdown
`` ``
## SPI
Increased throughput by 1.85 times, when working at the same frequency
SPI can now be configured and run in one line:
`` `c ++
StartSPI (0, 2, 1);
`` ``
Where the first parameter is the mode mode from 0 to 3, the second parameter is the clock divider, it can take the values ​​2, 4, 8, 16, 32, 64, 128. If you want to find out the SPI frequency, you must divide the controller clock frequency of 16000000 into any divider from the list. And the last parameter is which bit will go first. If 1, then the most significant bit goes first, if 0, then the least significant bit goes first.
`` `c ++
SendSPI (12); // Send a data byte to the SPI bus
MyData = ReadSPI (); // Get the data byte
StopSPI (); // Turn off SPI
`` ``
## EEPROM
** Constraint! ** Addresses a maximum of 256 addresses for type `byte`, for` word` maximum 128, for `long` maximum 64.

`` `c ++
WriteEEPROM_Long (0, 4000000); // Store the 4000000 value in the EEPROM at address 0, type Long
uint32_t tmp = ReadEEPROM_Long (0); // Read from the EEPROM from address 0 a value of type Long
WriteEEPROM_Word (0, 4000); // Store value 4000 in EEPROM at address 0 type Word
uint16_t tmp = ReadEEPROM_Word (0); // Read a Word type value from EEPROM from address 0
WriteEEPROM_Byte (0, 200); // Store the value 400 in the EEPROM at address 0 type Byte uint8_t tmp = ReadEEPROM_Byte (0); // Read Byte value from EEPROM from address 0
`` ``
## Filter for removing noise and false positives
`` `c ++
find_similar (Array, sizeArray, range);
`` ``
The function returns the most common value in the array.

Options:
* Array - Pointer to the array to be checked; the array can be of type `uint16_t` or` uint8_t`
* sizeArray - the length of the array is no more than 256 elements
* range - margin of error (deviation), can range from 0 to 127, with a value of 0, the function will look for exact copies of the values

## beep
`` `c ++
beep (uint16_t dur, uint16_t frq);
`` ``
Generates sound vibrations on any pin with a given frequency and duration.

Options:
* dur - duration from 50 ms to 65535 ms
* frq - frequency from 10 Hz to 2000 Hz

## Soft Reset
`` `c ++
reset (); // soft reset controller
`` ``
Using this function, you can send the controller to reboot anywhere in the program.

## Endless cycle
`` `c ++
Start // Start a loop
End // End of loop
`` ``

## Working with a watchdog
`` `c ++
wdt_reset (); // reset the watchdog timer
wdt_disable (); // turn off watchdog
wdt_enable (timeout); // Initialize Watchdog Timer
`` ``
### Possible timeout values
* `WDTO_15MS`
* `WDTO_30MS`
* `WDTO_60MS`
* `WDTO_120MS`
* `WDTO_250MS`
* `WDTO_500MS`
* `WDTO_1S`
* `WDTO_2S`
* `WDTO_4S`
* `WDTO_8S`

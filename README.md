# spiDebug_esp32s3
C++ class for debuging SPI problems on the ESP32-S3 SoC. 
Designed to work with the Arduino-IDE; but should also work with esptool.py
<br><br>
Useage :
<ol>
<li>If your arduino project doesn't have a `src` directory in it's root folder, create such a directory and put this code into there. (Unique to Arduino)</li>
<li>Include the header file in your code : `#include "./src/spiDebug_esp32/spiDebug.class.h"`</li>
<li>Define your variable : `SpiDebug spidbg;`</li>
<li>Set SPI Mode 2 or 3 (0 and 1 work; but shouldn't be used, default is SPI Mode 2) `spidbg.setMode(int mode)`
<li>Populate the SPI structs with either `spidbg.init()` or `spidbg.refresh()` the functions are identical.</li>
<li>Print out the registers as a whole or independantly. Doing `spidbg.printAll(false)` prints all the registers, `spidbg.printAll(true)` will </li>
</ol>
<br><br>
As of now, there is no automated register writes, but I did include a function that allows you to write to arbitrary SPI registers.

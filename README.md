# spiDebug_esp32s3
C++ class for debuging SPI problems on the ESP32-S3 SoC. 
Designed to work with the Arduino-IDE; but should also work with esptool.py
<br><br>
Useage :
<ol>
<li>If your arduino project doesn't have a <code>src</code> directory in it's root folder, create such a directory and put this code into there. (Unique to Arduino)</li>
<li>Include the header file in your code : <code>#include "./src/spiDebug_esp32/spiDebug.class.h"</code></li>
<li>Define your variable : <code>SpiDebug spidbg;</code></li>
<li>Set SPI Mode 2 or 3 (0 and 1 work; but shouldn't be used, default is SPI Mode 2) <code>SpiDebug::setMode(int mode)</code></li>
<li>Populate the SPI structs with either <code>SpiDebug::init()</code> or <code>SpiDebug::refresh()</code> the functions are identical.</li>
<li>Print out the registers as a whole or independantly. Doing <code>SpiDebug::printAll(false)</code> prints the registers in a decoded form, <code>SpiDebug::printAll(true)</code> will print out only single 32 bit register values for ease of config compairson.</li>
<li>Change SPI configurations by accessing the <code>SpiDebug::sr_*</code> registers. After changing, write the changes to the register using the <code>SpiDebug::patch*(true)</code> functions. Provide false to convert structs to a 32 bit register value without writing to the register (read only mode)</li>
</ol>

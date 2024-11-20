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

## Detecting configuration Changes
<p>
To detect changes in SPI configurations, use the following psudo code into consideration:</p>

```
SpiDebug dbgA;
SpiDebug dbgB;

dbgA.init();
dbgB.init();

EnableSomeSpiDevice();

dbgB.refresh();

dbgA.compAll(dbgB, true);
```

<p>
<br><br>
The above would produce a result similar to this:
</p>

```
~~~User Defined Register Compairisons~~~
spi_usr_miso (0x0) vs (0x1) <- cmp
spi_usr_mosi (0x0) vs (0x1) <- cmp
spi_doutdin (0x0) vs (0x1) <- cmp
spi_usr_command_bitlen (0x0) vs (0x7) <- cmp
spi_mst_rempty_err_end_en (0x0) vs (0x1) <- cmp
spi_ms_data_bitlen (0x0) vs (0x1ff) <- cmp
spi_ck_idle_edge (0x0) vs (0x1) <- cmp
spi_slv_tx_seg_trans_clr_en (0x0) vs (0x1) <- cmp
spi_slv_rx_seg_trans_clr_en (0x0) vs (0x1) <- cmp
spi_dma_infifo_full (0x0) vs (0x1) <- cmp
spi_dma_outfifo_empty (0x0) vs (0x1) <- cmp
```

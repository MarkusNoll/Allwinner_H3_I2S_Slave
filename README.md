# Allwinner H3 I2S-Slave Devicetree Overlay
Those are the resources to build up a bidrectional I2S slave interface on an Allwinner H3 SoC (I tested on a OrangePi One) running Armbian. <br>
It uses a custom dummy-codec driver and therefore it can be interfaced as dumb I²S interface to DSPs / FPGAs etc.. and doesn't expect an I²C codec being present. As it is a I2S-slave interface, the BCLK and WCLK must be supply externally to the H3 SoC.<br><br>
PA19 -> I2S-CLK<br>
PA18 -> I2S-WCLK<br>
PA20 -> I2S-OUT<br>
PA21 -> I2S-DIN
<br><br>
<b>First step:</b> Build the dummy-codec kernel-module. Just enter <b>$make</b> <br>
<b>Second step:</b> Build and install devicetree overlay with  <b>$armbian-add-overlay sun8i-h3-i2s0-slave.dts</b><br>
<b>Third step:</b> Reboot<br>
<b>Fourth step:</b> As the codec-kernel module is only compiled, but not installed, you have to load it manually with <b>$sudo insmod spdif-rxtx.ko</b><br><br>
Afterwards, you can check if the devices are present with <b>$aplay -l</b> or <b>$arecord -l</b>


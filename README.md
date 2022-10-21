# Allwinner H3 I2S-Slave Devicetree Overlay
Those are the resources to build up a bidrectional I2S slave interface on an Allwinner H3 SoC (I tested on a OrangePi One) running Armbian. <br>
It uses a custom dummy-codec driver and therefore it can be interfaced as dumb I²S interface to DSPs / FPGAs etc.. and doesn't expect an I²C codec being present. As it is a I2S-slave interface, the BCLK and WCLK must be supply externally to the H3 SoC.<br><br>
PA19 -> I2S-CLK<br>
PA18 -> I2S-WCLK<br>
PA20 -> I2S-OUT<br>
PA21 -> I2S-DIN
<br><br>
Firs step: Build the dummy-codec kernel-module. Just enter "$make" <br>
Second step: Build and install devicetree overlay with  "$armbian-add-overlay sun8i-h3-i2s0-slave.dts"<br>
Third step: Reboot
Fourth step: As the codec-kernel module is only compiled, but not installed, you have to load it manually with "$sudo insmod spdif-rxtx.ko"<br><br>
Afterwards, you can check if the devices are present with "$aplay -l" or "$arecord -l"


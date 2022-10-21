# Allwinner H3 I2S-Slave Devicetree Overlay
Those are the resources to build up a bidrectional I2S slave interface on an Allwinner H3 SoC (I tested on a OrangePi One) running Armbian. <br>
It uses a custom dummy-codec driver and therefore it can be interfaced as dumb I²S interface to DSPs / FPGAs etc.. and doesn't expect an I²C codec being present. As it is a I2S-slave interface, the BCLK and WCLK must be supply externally to the H3 SoC.<br><br>
PA19 -> I2S-CLK<br>
PA18 -> I2S-WCLK<br>
PA20 -> I2S-OUT<br>
PA21 -> I2S-DIN
<br><br>
<b>First step:</b> Build the dummy-codec kernel-module. Just enter <b>$make</b>. Make sure Kernel-Headers are available for your platform. <br>
<b>Second step:</b> Build and install devicetree overlay with  <b>$armbian-add-overlay sun8i-h3-i2s0-slave.dts</b><br>
<b>Third step:</b> Reboot<br>
<b>Fourth step:</b> As the codec-kernel module is only compiled, but not installed, you have to load it manually with <b>$sudo insmod spdif-rxtx.ko</b><br><br>
Afterwards, you can check if the devices are present with <b>$aplay -l</b> or <b>$arecord -l</b><br>
![Alsa IO](alsa-i2s.JPG?raw=true "Alsa IO")
<br><br>
Afterwards, try making a loopback with: <b>alsaloop -C hw:1,0 -P hw:1,0</b>...
<br><br>
In case you're playing something with MPV or record something, make sure you have set the correct sample-rate.<br>
<b>$ arecord -f S16_LE -r 48000 -c 2 -d 10 -D "hw:1,0" test.wav</b><br>

<b>$mpv https://edge01.stream.charivari.de/955charivari-webradio?aggregator=charivari_de_link --audio-display=no --audio-channels=stereo --audio-samplerate=48000 --audio-format=s32 --ao=alsa -audio-device=alsa/plughw:CARD=DAC,DEV=0</b>

---
layout:     post
title:      "The troubles of serial communication on a Mac"
date:       2016-06-10 12:00:00
author:     "Rohith H Y"
feature: "post-three.jpg"
imgurl: "https://img1.etsystatic.com/192/1/15691347/il_fullxfull.1310387223_lty9.jpg"
imgStyle: "display:block;margin:auto;width:60%;"
subtitle: "In this post I describe the simple solution of where you can find the USB/Serial devices on your mac."
---

<div class="entry-content">
	<p>In this post I describe the simple solution of where you can find the USB/Serial devices on your mac. All you really need to do is download the JSSC class on java first in order to be able to work with the device on java .&nbsp;The device I am using is a CP210x USB to UART that gives me serial data.</p>
    <p>So here’s what people would normally do :</p>
    <pre><code> String[] portNames = SerialPort.getPortNames("COM3");</code></pre>
    <p>Dear Mister Whoever,</p>
    <p>This is not going to work. Instead try :</p>
    <pre> Pattern pattern = Pattern.compile("tty.");
     String[] portNames = SerialPortList.getPortNames("/dev", pattern);</pre>
    <p>since this is where the usb devices show up on a Mac.</p>
    <p>You will have access to the portNames this way. Then you can proceed to read the serial data and have a jolly good day.<br>
    The next thing you do to read the data is :</p>
    <p>[ The below line is important as it points to the serial port. In windows you would give it as COM3 or the like. After that, the procedure is pretty much the same. This one line would have saved me a bunch of hours had I found it online. ]</p>
    <pre><code><strong>SerialPort serialPort = new SerialPort("/dev/tty.SLAB_USBtoUART");&nbsp;</strong>
     
     serialPort.openPort();
     serialPort.setParams(SerialPort.BAUDRATE_9600,
     SerialPort.DATABITS_8,
     SerialPort.STOPBITS_1,
     SerialPort.PARITY_NONE);</code></pre>
    <p>&nbsp;</p>
    <p>Rohith out.</p>
</div>
---
layout:     post
title:      "How to use the Bluetooth Low Energy API in Android"
date:       2016-07-08 12:00:00
author:     "Rohith H Y"
feature: "post-three.jpg"
subtitle: "I’ve been creating an application to monitor the atmospheric pollution using a Bluetooth LE device. Initially, it was a bit hard as I was overwhelmed with the number of options available but I was eventually able to figure out what needed to be done to establish a connection between the phone and device and extract the bluetooth data."
---

<div class="entry-content">
	<p>I’ve been creating an application to monitor the atmospheric pollution using a Bluetooth LE device. Initially, it was a bit hard as I was overwhelmed with the number of options available but I was eventually able to figure out what needed to be done to establish a connection between the phone and device and extract the bluetooth data.</p>
    <p>The below video helped a lot, it is very straightforward compared to a lot of the others and helped me in building my application :&nbsp;<span class="skimlinks-unlinked">https://www.youtube.com/watch?v=x1y4tEHDwk0&amp;list=PL2PAEHK-s-1UlXHzBhIP68yCsP8EOHgxJ</span></p>
    <p>1. Make your activity implement BluetoothAdapter.LeScanCallback</p>
    <pre><code>public class Main extends Activity implements BluetoothAdapter.LeScanCallback {</code></pre>
    <p>2. Get a&nbsp;reference to the bluetooth manager</p>
    <pre><code>BluetoothManager manager = (BluetoothManager) getSystemService(BLUETOOTH_SERVICE);
    mBluetoothAdapter = manager.getAdapter();</code></pre>
    <p>3. Have a “Start Scanning” &nbsp;button in your UI which when clicked would begin scanning for Bluetooth LE devices and “Stop Scanning” to stop scanning. When clicked, the corresponding methods below would be executed :</p>
    <pre><code>private void startScan(View view) {
    Toast.makeText(this, "Starting scan", Toast.LENGTH_SHORT).show();
    mBluetoothAdapter.startLeScan(this);
    }</code></pre>
    <pre><code>public void stopScan(View view) {
        Toast.makeText(this, "Stopping scan", Toast.LENGTH_SHORT).show();
        mBluetoothAdapter.stopLeScan(this);
    }</code></pre>
    <p style="text-align:center;">&nbsp; &nbsp; &nbsp; &nbsp; &nbsp; &nbsp;<img data-attachment-id="151" data-permalink="https://thehylifeblog.wordpress.com/2016/07/08/how-to-use-the-bluetooth-low-energy-api-in-android/screen-shot-2016-07-08-at-1-16-54-pm/" data-orig-file="https://thehylifeblog.files.wordpress.com/2016/07/screen-shot-2016-07-08-at-1-16-54-pm.png?w=348&amp;h=469" data-orig-size="180,243" data-comments-opened="1" data-image-meta="{&quot;aperture&quot;:&quot;0&quot;,&quot;credit&quot;:&quot;&quot;,&quot;camera&quot;:&quot;&quot;,&quot;caption&quot;:&quot;&quot;,&quot;created_timestamp&quot;:&quot;0&quot;,&quot;copyright&quot;:&quot;&quot;,&quot;focal_length&quot;:&quot;0&quot;,&quot;iso&quot;:&quot;0&quot;,&quot;shutter_speed&quot;:&quot;0&quot;,&quot;title&quot;:&quot;&quot;,&quot;orientation&quot;:&quot;0&quot;}" data-image-title="Screen Shot 2016-07-08 at 1.16.54 PM" data-image-description="" data-medium-file="https://thehylifeblog.files.wordpress.com/2016/07/screen-shot-2016-07-08-at-1-16-54-pm.png?w=348&amp;h=469?w=180" data-large-file="https://thehylifeblog.files.wordpress.com/2016/07/screen-shot-2016-07-08-at-1-16-54-pm.png?w=348&amp;h=469?w=180" class="alignnone  wp-image-151" src="https://thehylifeblog.files.wordpress.com/2016/07/screen-shot-2016-07-08-at-1-16-54-pm.png?w=348&amp;h=469" alt="Screen Shot 2016-07-08 at 1.16.54 PM" width="348" height="469" srcset="https://thehylifeblog.files.wordpress.com/2016/07/screen-shot-2016-07-08-at-1-16-54-pm.png 180w, https://thehylifeblog.files.wordpress.com/2016/07/screen-shot-2016-07-08-at-1-16-54-pm.png?w=111&amp;h=150 111w" sizes="(max-width: 348px) 100vw, 348px"></p>
    <p style="text-align:left;"><strong>Explanation</strong> : startLeScan and stopLeScan are methods of the BluetoothAdapter class which start or stop the scanning process when called.</p>
    <p style="text-align:left;">3. Now, whenever a device is located a call back function is executed from where you can extract its name, address and data that it is sending.</p>
    <pre><code>@Override
    public void onLeScan(BluetoothDevice device, int rssi, byte[] scanRecord) {
        <span class="skimlinks-unlinked">System.out.println("New</span>ce : " + device.getName() + " : " + device.getAddress());
        Toast.makeText(this,"New Device : " + device.getName() + " : " + device.getAddress(), Toast.LENGTH_SHORT).show();
    }</code></pre>
    <p style="text-align:left;"></p>
    <p style="text-align:left;">4. Now that the connection is established, you may proceed to operate on your data in the ways you wish.</p>
    <p style="text-align:left;"><strong>NOTE</strong>: The startLeScan &nbsp;and stopLeScan of the BluetoothAdapter class have been deprecated and replaced by other methods, please feel free to use them. I used them for this tutorial because they are unbelievably easy to use and I was able to add the desired functionality to my app successfully.</p>
    <p style="text-align:left;">
	</p>
	<div class="wpcnt"></div>			
</div>
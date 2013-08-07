---
layout: post
category : Ubuntu
tags : [Ubuntu, Wireless USB Adapter]
---
{% include JB/setup %}

<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 Install ndisgtk</a></li>
<li><a href="#sec-2">2 Download the inf drive file for windows from the offical site</a></li>
<li><a href="#sec-3">3 Open ndisgtk in dash and install the inf file</a></li>
<li><a href="#sec-4">4 Unknown problem</a></li>
</ul>
</div>
</div>

<div id="outline-container-1" class="outline-2">
<h2 id="sec-1">Install ndisgtk</h2>
<div class="outline-text-2" id="text-1">

<ul>
<li>sudo apt-get install ndisgtk
</li>
<li>If you get the source with apt-get (sudo apt-get install
    ndiswrapper-source) and install the module, you will get error:
    ‘struct kernel<sub>stat’</sub> has no member named ‘cpustat’. This
    error has been fixed in the latest version, and you have to
    download and install it manually.
</li>
<li>Download the latest module from <a href="http://sourceforge.net/projects/ndiswrapper/files/testing/">here</a>.
<ul>
<li>cd ndiswrapper-1.58rc1
</li>
<li>make
</li>
<li>sudo make install
</li>
</ul>

</li>
</ul>

</div>

</div>

<div id="outline-container-2" class="outline-2">
<h2 id="sec-2">Download the inf drive file for windows from the <a href="http://service.tp-link.com.cn/detail_download_991.html">offical site</a></h2>
<div class="outline-text-2" id="text-2">

<p>  Only the WinXp 32-bit version is needed.
</p></div>

</div>

<div id="outline-container-3" class="outline-2">
<h2 id="sec-3">Open ndisgtk in dash and install the inf file</h2>
<div class="outline-text-2" id="text-3">

<ul>
<li>Choose netrtwlanu.inf in ../WN725N 2.0/Driver Files/Windows XP
    32bit and install.
</li>
<li>If nidsgtk says that the hardware exists you are done.
</li>
</ul>

</div>

</div>

<div id="outline-container-4" class="outline-2">
<h2 id="sec-4"><span class="todo TODO">TODO</span> Unknown problem</h2>
<div class="outline-text-2" id="text-4">

<p>  If I close the switch for my laptop Wlan, the usb adapter is
  closed along with it. That won't happen in Windows.
</p></div>
</div>

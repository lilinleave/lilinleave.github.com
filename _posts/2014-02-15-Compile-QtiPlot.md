---
layout: post
category : software
tags : [QtiPlot]
---
{% include JB/setup %}

<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1. Python</a></li>
<li><a href="#sec-2">2. Other 3rdparty supports</a>
<ul>
<li><a href="#sec-2-1">2.1. Get the source</a></li>
<li><a href="#sec-2-2">2.2. The manual</a></li>
<li><a href="#sec-2-3">2.3. Others</a></li>
<li><a href="#sec-2-4">2.4. Copy files</a></li>
</ul>
</li>
<li><a href="#sec-3">3. Modifications</a>
<ul>
<li><a href="#sec-3-1">3.1. The build.conf file</a></li>
<li><a href="#sec-3-2">3.2. Bug in qwtplot3d</a></li>
<li><a href="#sec-3-3">3.3. Bugs in ImageWidget and FFT</a></li>
</ul>
</li>
<li><a href="#sec-4">4. Make</a>
<ul>
<li><a href="#sec-4-1">4.1. Missing QtAssistantClient</a></li>
<li><a href="#sec-4-2">4.2. Bug in sipqtiFFT</a></li>
</ul>
</li>
<li><a href="#sec-5">5. Make install</a></li>
</ul>
</div>
</div>

<p>
Finally I've successfully compiled the full-featrued <a href="http://soft.proindependent.com/qtiplot.html">QtiPlot</a>. There are some trivial bugs in the source. And it's time comsuming to prepare all the supports.
</p>

<div id="outline-container-sec-1" class="outline-2">
<h2 id="sec-1"><span class="section-number-2">1</span> Python</h2>
<div class="outline-text-2" id="text-1">
<p>
Qt4, Python, SIP and PyQt4 should be installed. To get the latter two:
</p>
<div class="org-src-container">

<pre class="src src-text">sudo apt-get install python-sip python-qt4
</pre>
</div>
</div>
</div>
<div id="outline-container-sec-2" class="outline-2">
<h2 id="sec-2"><span class="section-number-2">2</span> Other 3rdparty supports</h2>
<div class="outline-text-2" id="text-2">
</div><div id="outline-container-sec-2-1" class="outline-3">
<h3 id="sec-2-1"><span class="section-number-3">2.1</span> Get the source</h3>
<div class="outline-text-3" id="text-2-1">
<p>
Before the installation of other 3rdparty supports, download the source from the <a href="http://soft.proindependent.com/download.html">download page</a> (the <code>tar.bz2</code> file under 'QtiPlot cross platform source code') and extract it. There should be a 3rdparty directory, and the qwt, qwtplot3d, zlib supports are provided. I recommand that we copy all other needed include files and libs in the 3rdparty directory too. (The other way is to use the system directory)
</p>
</div>
</div>
<div id="outline-container-sec-2-2" class="outline-3">
<h3 id="sec-2-2"><span class="section-number-3">2.2</span> The manual</h3>
<div class="outline-text-3" id="text-2-2">
<p>
Docbook and dblatex are needed to generate the manual:
</p>
<div class="org-src-container">

<pre class="src src-text">sudo apt-get install docbook dblatex
</pre>
</div>
</div>
</div>
<div id="outline-container-sec-2-3" class="outline-3">
<h3 id="sec-2-3"><span class="section-number-3">2.3</span> Others</h3>
<div class="outline-text-3" id="text-2-3">
<p>
Then install the following supports:
</p>
<div class="org-src-container">

<pre class="src src-text">sudo apt-get install libmuparser-dev libtamuanova-dev libalglib-dev libqtexengine-dev libgsl0-dev libpng12-dev
</pre>
</div>
</div>
</div>
<div id="outline-container-sec-2-4" class="outline-3">
<h3 id="sec-2-4"><span class="section-number-3">2.4</span> Copy files</h3>
<div class="outline-text-3" id="text-2-4">
<p>
Under the root of the source file. First copy the <code>build.conf.example</code> file to <code>build.conf</code>. Open it and add in the first line the directory of the source, for example:
</p>
<div class="org-src-container">

<pre class="src src-text">QTI_ROOT = /home/yourname/src/qtiplot-0.9.8.9
</pre>
</div>

<p>
The following lines in this file tell you where you should copy support files to. Take muparser as an example:
</p>
<div class="org-src-container">

<pre class="src src-text">##########################################################
## muParser (http://muparser.sourceforge.net/)
##########################################################

# include path. leave it blank to use SYS_INCLUDE
MUPARSER_INCLUDEPATH = $$QTI_ROOT/3rdparty/muparser/include
# link statically against a copy in 3rdparty/
MUPARSER_LIBS = $$QTI_ROOT/3rdparty/muparser/lib/libmuparser.a
# or dynamically against a system-wide installation
#MUPARSER_LIBS = -lmuparser
</pre>
</div>
<p>
Thus the include files should be copied to 3rdparty/muparser/include, the lib should be copied to 3rdparty/muparser/lib.
</p>
<div class="org-src-container">

<pre class="src src-text">mkdir 3rdparty/muparser
mkdir 3rdparty/muparser/include
mkdir 3rdparty/muparser/lib
cp /usr/include/muParser/* 3rdparty/muparser/include
cp /usr/lib/libmuparser.so.0debian1.0.0 3rdparty/muparser/lib
mv 3rdparty/muparser/lib/libmuparser.so.0debian1.0.0 3rdparty/muparser/lib/libmuparser.a
</pre>
</div>
<p>
Other 3rdparty files should be copied likewise.
</p>
</div>
</div>
</div>
<div id="outline-container-sec-3" class="outline-2">
<h2 id="sec-3"><span class="section-number-2">3</span> Modifications</h2>
<div class="outline-text-2" id="text-3">
</div><div id="outline-container-sec-3-1" class="outline-3">
<h3 id="sec-3-1"><span class="section-number-3">3.1</span> The build.conf file</h3>
<div class="outline-text-3" id="text-3-1">
<p>
Two more modifications are needed for the <code>build.conf</code> file. First, since the 3rdparty supports are copied, the SYS<sub>INCLUDEPATH</sub> and SYS<sub>LIBS</sub> variables are not necessary. However there is a bug in the source that the GLU lib is not linked. Here we can add it to SYS<sub>LIBS</sub>: 
</p>
<div class="org-src-container">

<pre class="src src-text">SYS_LIBS = -lGLU
</pre>
</div>

<p>
If we want to install QtiPlot, we should also uncomment the line:
</p>
<div class="org-src-container">

<pre class="src src-text">#CONFIG          += CustomInstall
</pre>
</div>
</div>
</div>
<div id="outline-container-sec-3-2" class="outline-3">
<h3 id="sec-3-2"><span class="section-number-3">3.2</span> Bug in qwtplot3d</h3>
<div class="outline-text-3" id="text-3-2">
<p>
There is a bug in the file <code>3rdparty/qwtplot3d/include/qwt3d_openglhelper.h</code>, still GLU. Add in the include part this line:
</p>
<div class="org-src-container">

<pre class="src src-text">#include &lt;GL/glu.h&gt;
</pre>
</div>
</div>
</div>
<div id="outline-container-sec-3-3" class="outline-3">
<h3 id="sec-3-3"><span class="section-number-3">3.3</span> Bugs in ImageWidget and FFT</h3>
<div class="outline-text-3" id="text-3-3">
<p>
And a bug in the file <code>qtiplot/src/plot2D/ImageWidget.h</code>. The function <code>paintEvent(QPaintEvent *e)</code> should be public. Move the line:
</p>
<div class="org-src-container">

<pre class="src src-text">void paintEvent(QPaintEvent *e);
</pre>
</div>
<p>
from private to public.
</p>

<p>
Also a same bug in the file <code>qtiplot/src/analysis/FFT.h</code>. Move the line:
</p>
<div class="org-src-container">

<pre class="src src-text">bool setDataFromTable(Table *t, const QString&amp; realColName, const QString&amp; imagColName = QString(), int from = 0, int to = -1);
</pre>
</div>
<p>
from private to public.
</p>
</div>
</div>
</div>
<div id="outline-container-sec-4" class="outline-2">
<h2 id="sec-4"><span class="section-number-2">4</span> Make</h2>
<div class="outline-text-2" id="text-4">
<p>
Now start to make. 
</p>
<div class="org-src-container">

<pre class="src src-text">qmake
make
</pre>
</div>
<p>
Still two bugs might be waiting for you.
</p>
</div>

<div id="outline-container-sec-4-1" class="outline-3">
<h3 id="sec-4-1"><span class="section-number-3">4.1</span> Missing QtAssistantClient</h3>
<div class="outline-text-3" id="text-4-1">
<p>
In the 4.8 version Qt the QtAssistantClient is not included. Install it:
</p>
<div class="org-src-container">

<pre class="src src-text">sudo apt-get install libqtassistantclient-dev
</pre>
</div>
<p>
Then modify the Makefile in qtiplot (not the one under QTI<sub>ROOT</sub>). Find the line:
</p>
<div class="org-src-container">

<pre class="src src-text">INCPATH       = ......
</pre>
</div>
<p>
Add <code>-I/usr/include/qt4/QtAssistantClient</code> to the left.
</p>
</div>
</div>
<div id="outline-container-sec-4-2" class="outline-3">
<h3 id="sec-4-2"><span class="section-number-3">4.2</span> Bug in sipqtiFFT</h3>
<div class="outline-text-3" id="text-4-2">
<p>
This is a variable miss-match. A <code>tmp</code> directory under QTI<sub>ROOT</sub> is generated during compilation. Open the file <code>tmp/qtiplot/sipqtiFFT.cpp</code> and find the line:
</p>
<div class="org-src-container">

<pre class="src src-text">return FFT::setDataFromTable(a0,a1,a2,a3,a4,a5);
</pre>
</div>
<p>
Modify it to:
</p>
<div class="org-src-container">

<pre class="src src-text">return FFT::setDataFromTable(a0,a1,a2,a3,a4);
</pre>
</div>
</div>
</div>
</div>
<div id="outline-container-sec-5" class="outline-2">
<h2 id="sec-5"><span class="section-number-2">5</span> Make install</h2>
<div class="outline-text-2" id="text-5">
<p>
After the above procedure, now make should work. We can install:
</p>
<div class="org-src-container">

<pre class="src src-text">sudo make install
</pre>
</div>
<p>
However the Makefile under <code>manual</code> doesn't have a rule for install. We have to remove the corresponding part in the Makefile under QTI<sub>ROOT</sub>. Find the line:
</p>
<div class="org-src-container">

<pre class="src src-text">install_subtargets: sub-fitPlugins-install_subtargets sub-manual-install_subtargets sub-3rdparty-qwt-install_subtargets sub-3rdparty-qwtplot3d-install_subtargets sub-qtiplot-install_subtargets FORCE
</pre>
</div>
<p>
Delete <code>sub-manual-install_subtargets</code> from it.
</p>
</div>
</div>

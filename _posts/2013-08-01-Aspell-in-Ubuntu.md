---
layout: post
category : Ubuntu
tags : [Aspell, Flyspell, Emacs]
---
{% include JB/setup %}


<div id="table-of-contents">
<h2>Table of Contents</h2>
<div id="text-table-of-contents">
<ul>
<li><a href="#sec-1">1 Preface</a></li>
<li><a href="#sec-2">2 Fix error in Chinese Ubuntu</a>
<ul>
<li><a href="#sec-2-1">2.1 Set language for Aspell</a></li>
</ul>
</li>
<li><a href="#sec-3">3 Personal wordlist</a></li>
</ul>
</div>
</div>
<!-- more -->
<div id="outline-container-1" class="outline-2">
<h2 id="sec-1">Preface</h2>
<div class="outline-text-2" id="text-1">

<p>Flyspell is an Emacs minor-mode for spell check. Itself is not a spell check
tool but a front end which communicates with tools in your system. Many people
recommend Aspell as such a spell checking tool. Here is a memo of solutions to
two problems I met when using Aspell.
</p></div>

</div>

<div id="outline-container-2" class="outline-2">
<h2 id="sec-2">Fix error in Chinese Ubuntu</h2>
<div class="outline-text-2" id="text-2">

<p>If you are using Chinese Ubuntu (or other Chinese distribution I guess) you
might get error in Emacs when you enable Flyspell/Aspell which says:
</p>


<pre class="example">Error: No word lists can be found for the language "zh_CN"
</pre>

<p>
Almost every solution to this error you'll find on the Internet is to add the
following line to your .emacs:
</p>


<pre class="example">(ispell-change-dictionary "american" t)
</pre>

<p>
That will set your default dictionary for Flyspell to "american". However,
obviously the problem is not solved outside Emacs. In addition, other English
dictionaries are unavailable this way. The appropriate way, as you might
guess, is to set the language for Aspell to "en".
</p>
</div>

<div id="outline-container-2-1" class="outline-3">
<h3 id="sec-2-1">Set language for Aspell</h3>
<div class="outline-text-3" id="text-2-1">

<p>One thing that is still not clear to me is that, if you follow the command in
the <a href="http://aspell.net/man-html/">official manual</a> and try to customize Aspell in terminal, you'll not success.
And I managed to do it through the configuration file, which is .aspell.config
in your home directory or aspell.config in /etc. I recommend you to use the
latter to fix the error for all users. Just create aspell.config in /etc and
add
</p>


<pre class="example">lang en
</pre>

<p>
to it and you are done.
</p></div>
</div>

</div>

<div id="outline-container-3" class="outline-2">
<h2 id="sec-3">Personal wordlist</h2>
<div class="outline-text-2" id="text-3">

<p>Adding words to personal wordlist through terminal also doesn't work for me.
So create .aspell.en.pws in your home directory and add
</p>


<pre class="example">personal_ws-1.1 en 0
</pre>

<p>
to it, where 0 is the number of you words and 0 is fine no matter how much the
totality actually is. Then just add your wordlist below one word one line.
</p></div>
</div>

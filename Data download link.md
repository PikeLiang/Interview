<article class="markdown-body entry-content" itemprop="mainContentOfPage"><h1><a id="user-content-cn_mooc_dl" class="anchor" href="#cn_mooc_dl" aria-hidden="true"><span class="octicon octicon-link"></span></a>cn_mooc_dl</h1>

<ol>
<li>中国大学 MOOC（<code>icourse163.org</code>）视频下载</li>
<li>清华学堂在线（<code>xuetangx.com</code>）视频下载</li>
<li>网易云课堂（<code>study.163.com</code>）视频下载</li>
<li>网易云课堂计算机专业课程（<code>mooc.study.163.com</code>）视频下载</li>
</ol>

<h4><a id="user-content-测试环境---python-27-win-7" class="anchor" href="#测试环境---python-27-win-7" aria-hidden="true"><span class="octicon octicon-link"></span></a>测试环境：   <code>PYTHON 2.7； WIN 7</code></h4>

<h4><a id="user-content-依赖包-requests-beautifulsoup4" class="anchor" href="#依赖包-requests-beautifulsoup4" aria-hidden="true"><span class="octicon octicon-link"></span></a>依赖包： <code>requests， beautifulsoup4</code></h4>

<pre><code>pip install requests
pip install beautifulsoup4
</code></pre>

<p>或者在代码目录下</p>

<pre><code>pip install -r requirements.txt 
</code></pre>

<h4><a id="user-content-中国大学-moocicourse163org" class="anchor" href="#中国大学-moocicourse163org" aria-hidden="true"><span class="octicon octicon-link"></span></a>中国大学 MOOC（<code>icourse163.org</code>）：</h4>

<pre><code>python icourse163_dl.py  -u &lt;username@xxx.xxx&gt; -p &lt;password&gt;  "url"
</code></pre>

<ul>
<li>其中 url 是打开课程页面后，浏览器地址栏‘#’之前部分。
以“国防科大高等数学（一）”为例，打开课程后浏览器地址栏显示为：
<code>http://www.icourse163.org/learn/nudt-9004#/learn/announce</code>
则 url 为 <code>http://www.icourse163.org/learn/nudt-9004</code></li>
<li>网易流量时快时慢，时有时无。可以运行两遍，之前没下完的可断线续传。</li>
</ul>

<h4><a id="user-content-清华学堂在线xuetangxcom" class="anchor" href="#清华学堂在线xuetangxcom" aria-hidden="true"><span class="octicon octicon-link"></span></a>清华学堂在线（<code>xuetangx.com</code>）：</h4>

<pre><code>python xuetangx_dl.py  -u &lt;username@xxx.xxx&gt; -p &lt;password&gt;  "url"
</code></pre>

<ul>
<li>其中 url 是课程课件页面的浏览器地址，比如：
<code>http://www.xuetangx.com/courses/HITx/GO90300700/2014_T2/courseware/</code></li>
</ul>

<h4><a id="user-content-网易云课堂study163com" class="anchor" href="#网易云课堂study163com" aria-hidden="true"><span class="octicon octicon-link"></span></a>网易云课堂（<code>study.163.com</code>）：</h4>

<pre><code>python study163_dl.py "url"
</code></pre>

<ul>
<li>云课堂新增专栏“计算机专业课程”那一部分（mooc.study.163.com）有点特殊，具体看下面。</li>
<li>收费课程下不了。</li>
<li>网易云课堂不必登录。其中 url 是课程列表页面浏览器地址，比如:
<code>http://study.163.com/course/introduction/334013.htm</code></li>
<li>不能续传。</li>
</ul>

<h4><a id="user-content-云课堂计算机专业课程moocstudy163com" class="anchor" href="#云课堂计算机专业课程moocstudy163com" aria-hidden="true"><span class="octicon octicon-link"></span></a>云课堂计算机专业课程（<code>mooc.study.163.com</code>）：</h4>

<pre><code>python icourse163_dl.py  -u &lt;username@xxx.xxx&gt; -p &lt;password&gt;  "url" 
</code></pre>

<ul>
<li>云课堂新增专栏“计算机专业课程”，虽然挂在云课堂页面上，但是里面的结构是和“中国大学 MOOC”一样的。所以要用 <code>icourse163_dl.py</code> 来下载。</li>
<li>其中 url 类似这样： <code>http://mooc.study.163.com/learn/ZJU-1000002014</code></li>
</ul>

<h5><a id="user-content---path-用于指定保存文件夹---overwrite-指定是否覆盖" class="anchor" href="#--path-用于指定保存文件夹---overwrite-指定是否覆盖" aria-hidden="true"><span class="octicon octicon-link"></span></a>--path 用于指定保存文件夹， --overwrite 指定是否覆盖</h5>

<p><a href="mailto:liangsenzhi@gmail.com">liangsenzhi@gmail.com</a></p>
</article>
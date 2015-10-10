<article class="markdown-body entry-content" itemprop="mainContentOfPage"><h1><a id="user-content-javascript规范" class="anchor" href="#javascript规范" aria-hidden="true"><span class="octicon octicon-link"></span></a>JavaScript规范</h1>

<h2><a id="user-content-类型" class="anchor" href="#类型" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-types">类型</a></h2>

<ul>
<li><p><strong>原始值</strong>: 相当于传值</p>

<ul>
<li><code>string</code></li>
<li><code>number</code></li>
<li><code>boolean</code></li>
<li><code>null</code></li>
<li><code>undefined</code></li>
</ul>

<div class="highlight highlight-source-js"><pre><span class="pl-k">var</span> foo <span class="pl-k">=</span> <span class="pl-c1">1</span>,
    bar <span class="pl-k">=</span> foo;

bar <span class="pl-k">=</span> <span class="pl-c1">9</span>;

<span class="pl-en">console</span>.<span class="pl-c1">log</span>(foo, bar); <span class="pl-c">// =&gt; 1, 9</span></pre></div></li>
<li><p><strong>复杂类型</strong>: 相当于传引用</p>

<ul>
<li><code>object</code></li>
<li><code>array</code></li>
<li><code>function</code></li>
</ul>

<div class="highlight highlight-source-js"><pre><span class="pl-k">var</span> foo <span class="pl-k">=</span> [<span class="pl-c1">1</span>, <span class="pl-c1">2</span>],
    bar <span class="pl-k">=</span> foo;

bar[<span class="pl-c1">0</span>] <span class="pl-k">=</span> <span class="pl-c1">9</span>;

<span class="pl-en">console</span>.<span class="pl-c1">log</span>(foo[<span class="pl-c1">0</span>], bar[<span class="pl-c1">0</span>]); <span class="pl-c">// =&gt; 9, 9</span></pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-对象" class="anchor" href="#对象" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-objects">对象</a></h2>

<ul>
<li><p>使用字面值创建对象</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">var</span> item <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">Object</span>();

<span class="pl-c">// good</span>
<span class="pl-k">var</span> item <span class="pl-k">=</span> {};</pre></div></li>
<li><p>不要使用保留字 <a href="https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Reserved_Words">reserved words</a> 作为键</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">var</span> superman <span class="pl-k">=</span> {
  class<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>superhero<span class="pl-pds">'</span></span>,
  <span class="pl-k">default</span><span class="pl-k">:</span> { clark<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>kent<span class="pl-pds">'</span></span> },
  private<span class="pl-k">:</span> <span class="pl-c1">true</span>
};

<span class="pl-c">// good</span>
<span class="pl-k">var</span> superman <span class="pl-k">=</span> {
  klass<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>superhero<span class="pl-pds">'</span></span>,
  defaults<span class="pl-k">:</span> { clark<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>kent<span class="pl-pds">'</span></span> },
  hidden<span class="pl-k">:</span> <span class="pl-c1">true</span>
};</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-数组" class="anchor" href="#数组" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-arrays">数组</a></h2>

<ul>
<li><p>使用字面值创建数组</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">var</span> items <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">Array</span>();

<span class="pl-c">// good</span>
<span class="pl-k">var</span> items <span class="pl-k">=</span> [];</pre></div></li>
<li><p>如果你不知道数组的长度，使用push</p>

<div class="highlight highlight-source-js"><pre><span class="pl-k">var</span> someStack <span class="pl-k">=</span> [];


<span class="pl-c">// bad</span>
someStack[someStack.<span class="pl-c1">length</span>] <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>abracadabra<span class="pl-pds">'</span></span>;

<span class="pl-c">// good</span>
someStack.<span class="pl-c1">push</span>(<span class="pl-s"><span class="pl-pds">'</span>abracadabra<span class="pl-pds">'</span></span>);</pre></div></li>
<li><p>当你需要拷贝数组时使用slice. <a href="http://jsperf.com/converting-arguments-to-an-array/7">jsPerf</a></p>

<div class="highlight highlight-source-js"><pre><span class="pl-k">var</span> len <span class="pl-k">=</span> items.<span class="pl-c1">length</span>,
    itemsCopy <span class="pl-k">=</span> [],
    i;

<span class="pl-c">// bad</span>
<span class="pl-k">for</span> (i <span class="pl-k">=</span> <span class="pl-c1">0</span>; i <span class="pl-k">&lt;</span> len; i<span class="pl-k">++</span>) {
  itemsCopy[i] <span class="pl-k">=</span> items[i];
}

<span class="pl-c">// good</span>
itemsCopy <span class="pl-k">=</span> items.<span class="pl-c1">slice</span>();</pre></div></li>
<li><p>使用slice将类数组的对象转成数组.</p>

<div class="highlight highlight-source-js"><pre><span class="pl-k">function</span> <span class="pl-en">trigger</span>() {
  <span class="pl-k">var</span> args <span class="pl-k">=</span> <span class="pl-c1">Array</span>.<span class="pl-c1">prototype</span>.slice.<span class="pl-c1">call</span>(arguments);
  ...
}</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-字符串" class="anchor" href="#字符串" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-strings">字符串</a></h2>

<ul>
<li><p>对字符串使用单引号 <code>''</code></p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">var</span> name <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">"</span>Bob Parr<span class="pl-pds">"</span></span>;

<span class="pl-c">// good</span>
<span class="pl-k">var</span> name <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>Bob Parr<span class="pl-pds">'</span></span>;

<span class="pl-c">// bad</span>
<span class="pl-k">var</span> fullName <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">"</span>Bob <span class="pl-pds">"</span></span> <span class="pl-k">+</span> <span class="pl-v">this</span>.lastName;

<span class="pl-c">// good</span>
<span class="pl-k">var</span> fullName <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>Bob <span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-v">this</span>.lastName;</pre></div></li>
<li><p>超过80个字符的字符串应该使用字符串连接换行</p></li>
<li><p>注: 如果过度使用，长字符串连接可能会对性能有影响. <a href="http://jsperf.com/ya-string-concat">jsPerf</a> &amp; <a href="https://github.com/airbnb/javascript/issues/40">Discussion</a></p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">var</span> errorMessage <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>This is a super long error that was thrown because of Batman. When you stop to think about how Batman had anything to do with this, you would get nowhere fast.<span class="pl-pds">'</span></span>;

<span class="pl-c">// bad</span>
<span class="pl-k">var</span> errorMessage <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>This is a super long error that \</span>
<span class="pl-s">was thrown because of Batman. \</span>
<span class="pl-s">When you stop to think about \</span>
<span class="pl-s">how Batman had anything to do \</span>
<span class="pl-s">with this, you would get nowhere \</span>
<span class="pl-s">fast.<span class="pl-pds">'</span></span>;


<span class="pl-c">// good</span>
<span class="pl-k">var</span> errorMessage <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>This is a super long error that <span class="pl-pds">'</span></span> <span class="pl-k">+</span>
  <span class="pl-s"><span class="pl-pds">'</span>was thrown because of Batman.<span class="pl-pds">'</span></span> <span class="pl-k">+</span>
  <span class="pl-s"><span class="pl-pds">'</span>When you stop to think about <span class="pl-pds">'</span></span> <span class="pl-k">+</span>
  <span class="pl-s"><span class="pl-pds">'</span>how Batman had anything to do <span class="pl-pds">'</span></span> <span class="pl-k">+</span>
  <span class="pl-s"><span class="pl-pds">'</span>with this, you would get nowhere <span class="pl-pds">'</span></span> <span class="pl-k">+</span>
  <span class="pl-s"><span class="pl-pds">'</span>fast.<span class="pl-pds">'</span></span>;</pre></div></li>
<li><p>编程时使用join而不是字符串连接来构建字符串，特别是IE: <a href="http://jsperf.com/string-vs-array-concat/2">jsPerf</a>.</p>

<div class="highlight highlight-source-js"><pre><span class="pl-k">var</span> items,
    messages,
    length, i;

messages <span class="pl-k">=</span> [{
    state<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>success<span class="pl-pds">'</span></span>,
    message<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>This one worked.<span class="pl-pds">'</span></span>
},{
    state<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>success<span class="pl-pds">'</span></span>,
    message<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>This one worked as well.<span class="pl-pds">'</span></span>
},{
    state<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>error<span class="pl-pds">'</span></span>,
    message<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>This one did not work.<span class="pl-pds">'</span></span>
}];

length <span class="pl-k">=</span> messages.<span class="pl-c1">length</span>;

<span class="pl-c">// bad</span>
<span class="pl-k">function</span> <span class="pl-en">inbox</span>(<span class="pl-smi">messages</span>) {
  items <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>&lt;ul&gt;<span class="pl-pds">'</span></span>;

  <span class="pl-k">for</span> (i <span class="pl-k">=</span> <span class="pl-c1">0</span>; i <span class="pl-k">&lt;</span> length; i<span class="pl-k">++</span>) {
    items <span class="pl-k">+=</span> <span class="pl-s"><span class="pl-pds">'</span>&lt;li&gt;<span class="pl-pds">'</span></span> <span class="pl-k">+</span> messages[i].message <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>&lt;/li&gt;<span class="pl-pds">'</span></span>;
  }

  <span class="pl-k">return</span> items <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>&lt;/ul&gt;<span class="pl-pds">'</span></span>;
}

<span class="pl-c">// good</span>
<span class="pl-k">function</span> <span class="pl-en">inbox</span>(<span class="pl-smi">messages</span>) {
  items <span class="pl-k">=</span> [];

  <span class="pl-k">for</span> (i <span class="pl-k">=</span> <span class="pl-c1">0</span>; i <span class="pl-k">&lt;</span> length; i<span class="pl-k">++</span>) {
    items[i] <span class="pl-k">=</span> messages[i].message;
  }

  <span class="pl-k">return</span> <span class="pl-s"><span class="pl-pds">'</span>&lt;ul&gt;&lt;li&gt;<span class="pl-pds">'</span></span> <span class="pl-k">+</span> items.<span class="pl-c1">join</span>(<span class="pl-s"><span class="pl-pds">'</span>&lt;/li&gt;&lt;li&gt;<span class="pl-pds">'</span></span>) <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>&lt;/li&gt;&lt;/ul&gt;<span class="pl-pds">'</span></span>;
}</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-函数" class="anchor" href="#函数" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-functions">函数</a></h2>

<ul>
<li><p>函数表达式:</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// 匿名函数表达式</span>
<span class="pl-k">var</span> <span class="pl-en">anonymous</span> <span class="pl-k">=</span> <span class="pl-k">function</span>() {
  <span class="pl-k">return</span> <span class="pl-c1">true</span>;
};

<span class="pl-c">// 有名函数表达式</span>
<span class="pl-k">var</span> <span class="pl-en">named</span> <span class="pl-k">=</span> <span class="pl-k">function</span> <span class="pl-en">named</span>() {
  <span class="pl-k">return</span> <span class="pl-c1">true</span>;
};

<span class="pl-c">// 立即调用函数表达式</span>
(<span class="pl-k">function</span>() {
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>Welcome to the Internet. Please follow me.<span class="pl-pds">'</span></span>);
})();</pre></div></li>
<li><p>绝对不要在一个非函数块里声明一个函数，把那个函数赋给一个变量。浏览器允许你这么做，但是它们解析不同。</p></li>
<li><p><strong>注:</strong> ECMA-262定义把<code>块</code>定义为一组语句，函数声明不是一个语句。<a href="http://www.ecma-international.org/publications/files/ECMA-ST/Ecma-262.pdf#page=97">阅读ECMA-262对这个问题的说明</a>.</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">if</span> (currentUser) {
  <span class="pl-k">function</span> <span class="pl-en">test</span>() {
    <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>Nope.<span class="pl-pds">'</span></span>);
  }
}

<span class="pl-c">// good</span>
<span class="pl-k">if</span> (currentUser) {
  <span class="pl-k">var</span> <span class="pl-en">test</span> <span class="pl-k">=</span> <span class="pl-k">function</span> <span class="pl-en">test</span>() {
    <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>Yup.<span class="pl-pds">'</span></span>);
  };
}</pre></div></li>
<li><p>绝对不要把参数命名为 <code>arguments</code>, 这将会逾越函数作用域内传过来的 <code>arguments</code> 对象.</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">function</span> <span class="pl-en">nope</span>(<span class="pl-smi">name</span>, <span class="pl-smi">options</span>, <span class="pl-smi">arguments</span>) {
  <span class="pl-c">// ...stuff...</span>
}

<span class="pl-c">// good</span>
<span class="pl-k">function</span> <span class="pl-en">yup</span>(<span class="pl-smi">name</span>, <span class="pl-smi">options</span>, <span class="pl-smi">args</span>) {
  <span class="pl-c">// ...stuff...</span>
}</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-属性" class="anchor" href="#属性" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-properties">属性</a></h2>

<ul>
<li><p>当使用变量访问属性时使用中括号.</p>

<div class="highlight highlight-source-js"><pre><span class="pl-k">var</span> luke <span class="pl-k">=</span> {
  jedi<span class="pl-k">:</span> <span class="pl-c1">true</span>,
  age<span class="pl-k">:</span> <span class="pl-c1">28</span>
};

<span class="pl-k">function</span> <span class="pl-en">getProp</span>(<span class="pl-smi">prop</span>) {
  <span class="pl-k">return</span> luke[prop];
}

<span class="pl-k">var</span> isJedi <span class="pl-k">=</span> getProp(<span class="pl-s"><span class="pl-pds">'</span>jedi<span class="pl-pds">'</span></span>);</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-变量" class="anchor" href="#变量" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-variables">变量</a></h2>

<ul>
<li><p>总是使用 <code>var</code> 来声明变量，如果不这么做将导致产生全局变量，我们要避免污染全局命名空间。</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
superPower <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">SuperPower</span>();

<span class="pl-c">// good</span>
<span class="pl-k">var</span> superPower <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">SuperPower</span>();</pre></div></li>
<li><p>使用一个 <code>var</code> 以及新行声明多个变量，缩进4个空格。</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">var</span> items <span class="pl-k">=</span> getItems();
<span class="pl-k">var</span> goSportsTeam <span class="pl-k">=</span> <span class="pl-c1">true</span>;
<span class="pl-k">var</span> dragonball <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>z<span class="pl-pds">'</span></span>;

<span class="pl-c">// good</span>
<span class="pl-k">var</span> items <span class="pl-k">=</span> getItems(),
    goSportsTeam <span class="pl-k">=</span> <span class="pl-c1">true</span>,
    dragonball <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>z<span class="pl-pds">'</span></span>;</pre></div></li>
<li><p>最后再声明未赋值的变量，当你想引用之前已赋值变量的时候很有用。</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">var</span> i, len, dragonball,
    items <span class="pl-k">=</span> getItems(),
    goSportsTeam <span class="pl-k">=</span> <span class="pl-c1">true</span>;

<span class="pl-c">// bad</span>
<span class="pl-k">var</span> i, items <span class="pl-k">=</span> getItems(),
    dragonball,
    goSportsTeam <span class="pl-k">=</span> <span class="pl-c1">true</span>,
    len;

<span class="pl-c">// good</span>
<span class="pl-k">var</span> items <span class="pl-k">=</span> getItems(),
    goSportsTeam <span class="pl-k">=</span> <span class="pl-c1">true</span>,
    dragonball,
    length,
    i;</pre></div></li>
<li><p>在作用域顶部声明变量，避免变量声明和赋值引起的相关问题。</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">function</span>() {
  <span class="pl-c1">test</span>();
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>doing stuff..<span class="pl-pds">'</span></span>);

  <span class="pl-c">//..other stuff..</span>

  <span class="pl-k">var</span> name <span class="pl-k">=</span> getName();

  <span class="pl-k">if</span> (name <span class="pl-k">===</span> <span class="pl-s"><span class="pl-pds">'</span>test<span class="pl-pds">'</span></span>) {
    <span class="pl-k">return</span> <span class="pl-c1">false</span>;
  }

  <span class="pl-k">return</span> name;
}

<span class="pl-c">// good</span>
<span class="pl-k">function</span>() {
  <span class="pl-k">var</span> name <span class="pl-k">=</span> getName();

  <span class="pl-c1">test</span>();
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>doing stuff..<span class="pl-pds">'</span></span>);

  <span class="pl-c">//..other stuff..</span>

  <span class="pl-k">if</span> (name <span class="pl-k">===</span> <span class="pl-s"><span class="pl-pds">'</span>test<span class="pl-pds">'</span></span>) {
    <span class="pl-k">return</span> <span class="pl-c1">false</span>;
  }

  <span class="pl-k">return</span> name;
}

<span class="pl-c">// bad</span>
<span class="pl-k">function</span>() {
  <span class="pl-k">var</span> name <span class="pl-k">=</span> getName();

  <span class="pl-k">if</span> (<span class="pl-k">!</span>arguments.<span class="pl-c1">length</span>) {
    <span class="pl-k">return</span> <span class="pl-c1">false</span>;
  }

  <span class="pl-k">return</span> <span class="pl-c1">true</span>;
}

<span class="pl-c">// good</span>
<span class="pl-k">function</span>() {
  <span class="pl-k">if</span> (<span class="pl-k">!</span>arguments.<span class="pl-c1">length</span>) {
    <span class="pl-k">return</span> <span class="pl-c1">false</span>;
  }

  <span class="pl-k">var</span> name <span class="pl-k">=</span> getName();

  <span class="pl-k">return</span> <span class="pl-c1">true</span>;
}</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-条件表达式和等号" class="anchor" href="#条件表达式和等号" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-conditionals">条件表达式和等号</a></h2>

<ul>
<li>适当使用 <code>===</code> 和 <code>!==</code> 以及 <code>==</code> 和 <code>!=</code>.</li>
<li><p>条件表达式的强制类型转换遵循以下规则：</p>

<ul>
<li><strong>对象</strong> 被计算为 <strong>true</strong></li>
<li><strong>Undefined</strong> 被计算为 <strong>false</strong></li>
<li><strong>Null</strong> 被计算为 <strong>false</strong></li>
<li><strong>布尔值</strong> 被计算为 <strong>布尔的值</strong></li>
<li><strong>数字</strong> 如果是 <strong>+0, -0, or NaN</strong> 被计算为 <strong>false</strong> , 否则为 <strong>true</strong></li>
<li><strong>字符串</strong> 如果是空字符串 <code>''</code> 则被计算为 <strong>false</strong>, 否则为 <strong>true</strong></li>
</ul>

<div class="highlight highlight-source-js"><pre><span class="pl-k">if</span> ([<span class="pl-c1">0</span>]) {
  <span class="pl-c">// true</span>
  <span class="pl-c">// An array is an object, objects evaluate to true</span>
}</pre></div></li>
<li><p>使用快捷方式.</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">if</span> (name <span class="pl-k">!==</span> <span class="pl-s"><span class="pl-pds">'</span><span class="pl-pds">'</span></span>) {
  <span class="pl-c">// ...stuff...</span>
}

<span class="pl-c">// good</span>
<span class="pl-k">if</span> (name) {
  <span class="pl-c">// ...stuff...</span>
}

<span class="pl-c">// bad</span>
<span class="pl-k">if</span> (collection.<span class="pl-c1">length</span> <span class="pl-k">&gt;</span> <span class="pl-c1">0</span>) {
  <span class="pl-c">// ...stuff...</span>
}

<span class="pl-c">// good</span>
<span class="pl-k">if</span> (collection.<span class="pl-c1">length</span>) {
  <span class="pl-c">// ...stuff...</span>
}</pre></div></li>
<li><p>阅读 <a href="http://javascriptweblog.wordpress.com/2011/02/07/truth-equality-and-javascript/#more-2108">Truth Equality and JavaScript</a> 了解更多</p>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-块" class="anchor" href="#块" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-blocks">块</a></h2>

<ul>
<li><p>给所有多行的块使用大括号</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">if</span> (test)
  <span class="pl-k">return</span> <span class="pl-c1">false</span>;

<span class="pl-c">// good</span>
<span class="pl-k">if</span> (test) <span class="pl-k">return</span> <span class="pl-c1">false</span>;

<span class="pl-c">// good</span>
<span class="pl-k">if</span> (test) {
  <span class="pl-k">return</span> <span class="pl-c1">false</span>;
}

<span class="pl-c">// bad</span>
<span class="pl-k">function</span>() { <span class="pl-k">return</span> <span class="pl-c1">false</span>; }

<span class="pl-c">// good</span>
<span class="pl-k">function</span>() {
  <span class="pl-k">return</span> <span class="pl-c1">false</span>;
}</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-注释" class="anchor" href="#注释" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-comments">注释</a></h2>

<ul>
<li><p>使用 <code>/** ... */</code> 进行多行注释，包括描述，指定类型以及参数值和返回值</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-c">// make() returns a new element</span>
<span class="pl-c">// based on the passed in tag name</span>
<span class="pl-c">//</span>
<span class="pl-c">// @param &lt;String&gt; tag</span>
<span class="pl-c">// @return &lt;Element&gt; element</span>
<span class="pl-k">function</span> <span class="pl-en">make</span>(<span class="pl-smi">tag</span>) {

  <span class="pl-c">// ...stuff...</span>

  <span class="pl-k">return</span> element;
}

<span class="pl-c">// good</span>
<span class="pl-c">/**</span>
<span class="pl-c"> * make() returns a new element</span>
<span class="pl-c"> * based on the passed in tag name</span>
<span class="pl-c"> *</span>
<span class="pl-c"> * <span class="pl-k">@param</span> &lt;String&gt; tag</span>
<span class="pl-c"> * <span class="pl-k">@return</span> &lt;Element&gt; element</span>
<span class="pl-c"> */</span>
<span class="pl-k">function</span> <span class="pl-en">make</span>(<span class="pl-smi">tag</span>) {

  <span class="pl-c">// ...stuff...</span>

  <span class="pl-k">return</span> element;
}</pre></div></li>
<li><p>使用 <code>//</code> 进行单行注释，在评论对象的上面进行单行注释，注释前放一个空行.</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">var</span> active <span class="pl-k">=</span> <span class="pl-c1">true</span>;  <span class="pl-c">// is current tab</span>

<span class="pl-c">// good</span>
<span class="pl-c">// is current tab</span>
<span class="pl-k">var</span> active <span class="pl-k">=</span> <span class="pl-c1">true</span>;

<span class="pl-c">// bad</span>
<span class="pl-k">function</span> <span class="pl-en">getType</span>() {
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>fetching type...<span class="pl-pds">'</span></span>);
  <span class="pl-c">// set the default type to 'no type'</span>
  <span class="pl-k">var</span> type <span class="pl-k">=</span> <span class="pl-v">this</span>._type <span class="pl-k">||</span> <span class="pl-s"><span class="pl-pds">'</span>no type<span class="pl-pds">'</span></span>;

  <span class="pl-k">return</span> type;
}

<span class="pl-c">// good</span>
<span class="pl-k">function</span> <span class="pl-en">getType</span>() {
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>fetching type...<span class="pl-pds">'</span></span>);

  <span class="pl-c">// set the default type to 'no type'</span>
  <span class="pl-k">var</span> type <span class="pl-k">=</span> <span class="pl-v">this</span>._type <span class="pl-k">||</span> <span class="pl-s"><span class="pl-pds">'</span>no type<span class="pl-pds">'</span></span>;

  <span class="pl-k">return</span> type;
}</pre></div></li>
<li><p>如果你有一个问题需要重新来看一下或如果你建议一个需要被实现的解决方法的话需要在你的注释前面加上 <code>FIXME</code> 或 <code>TODO</code> 帮助其他人迅速理解</p>

<div class="highlight highlight-source-js"><pre><span class="pl-k">function</span> <span class="pl-en">Calculator</span>() {

  <span class="pl-c">// FIXME: shouldn't use a global here</span>
  total <span class="pl-k">=</span> <span class="pl-c1">0</span>;

  <span class="pl-k">return</span> <span class="pl-v">this</span>;
}</pre></div>

<div class="highlight highlight-source-js"><pre><span class="pl-k">function</span> <span class="pl-en">Calculator</span>() {

  <span class="pl-c">// TODO: total should be configurable by an options param</span>
  <span class="pl-v">this</span>.total <span class="pl-k">=</span> <span class="pl-c1">0</span>;

  <span class="pl-k">return</span> <span class="pl-v">this</span>;
}</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-空白" class="anchor" href="#空白" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-whitespace">空白</a></h2>

<ul>
<li><p>将tab设为4个空格</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">function</span>() {
∙∙<span class="pl-k">var</span> name;
}

<span class="pl-c">// bad</span>
<span class="pl-k">function</span>() {
∙<span class="pl-k">var</span> name;
}

<span class="pl-c">// good</span>
<span class="pl-k">function</span>() {
∙∙∙∙<span class="pl-k">var</span> name;
}</pre></div></li>
<li><p>大括号前放一个空格</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">function</span> <span class="pl-en">test</span>(){
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>test<span class="pl-pds">'</span></span>);
}

<span class="pl-c">// good</span>
<span class="pl-k">function</span> <span class="pl-en">test</span>() {
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>test<span class="pl-pds">'</span></span>);
}

<span class="pl-c">// bad</span>
dog.set(<span class="pl-s"><span class="pl-pds">'</span>attr<span class="pl-pds">'</span></span>,{
  age<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>1 year<span class="pl-pds">'</span></span>,
  breed<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Bernese Mountain Dog<span class="pl-pds">'</span></span>
});

<span class="pl-c">// good</span>
dog.set(<span class="pl-s"><span class="pl-pds">'</span>attr<span class="pl-pds">'</span></span>, {
  age<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>1 year<span class="pl-pds">'</span></span>,
  breed<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Bernese Mountain Dog<span class="pl-pds">'</span></span>
});</pre></div></li>
<li><p>在做长方法链时使用缩进.</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
$(<span class="pl-s"><span class="pl-pds">'</span>#items<span class="pl-pds">'</span></span>).<span class="pl-c1">find</span>(<span class="pl-s"><span class="pl-pds">'</span>.selected<span class="pl-pds">'</span></span>).highlight().end().<span class="pl-c1">find</span>(<span class="pl-s"><span class="pl-pds">'</span>.open<span class="pl-pds">'</span></span>).updateCount();

<span class="pl-c">// good</span>
$(<span class="pl-s"><span class="pl-pds">'</span>#items<span class="pl-pds">'</span></span>)
  .<span class="pl-c1">find</span>(<span class="pl-s"><span class="pl-pds">'</span>.selected<span class="pl-pds">'</span></span>)
    .highlight()
    .end()
  .<span class="pl-c1">find</span>(<span class="pl-s"><span class="pl-pds">'</span>.open<span class="pl-pds">'</span></span>)
    .updateCount();

<span class="pl-c">// bad</span>
<span class="pl-k">var</span> leds <span class="pl-k">=</span> stage.selectAll(<span class="pl-s"><span class="pl-pds">'</span>.led<span class="pl-pds">'</span></span>).<span class="pl-c1">data</span>(data).enter().append(<span class="pl-s"><span class="pl-pds">'</span>svg:svg<span class="pl-pds">'</span></span>).class(<span class="pl-s"><span class="pl-pds">'</span>led<span class="pl-pds">'</span></span>, <span class="pl-c1">true</span>)
    .attr(<span class="pl-s"><span class="pl-pds">'</span>width<span class="pl-pds">'</span></span>,  (radius <span class="pl-k">+</span> margin) <span class="pl-k">*</span> <span class="pl-c1">2</span>).append(<span class="pl-s"><span class="pl-pds">'</span>svg:g<span class="pl-pds">'</span></span>)
    .attr(<span class="pl-s"><span class="pl-pds">'</span>transform<span class="pl-pds">'</span></span>, <span class="pl-s"><span class="pl-pds">'</span>translate(<span class="pl-pds">'</span></span> <span class="pl-k">+</span> (radius <span class="pl-k">+</span> margin) <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>,<span class="pl-pds">'</span></span> <span class="pl-k">+</span> (radius <span class="pl-k">+</span> margin) <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>)<span class="pl-pds">'</span></span>)
    .<span class="pl-c1">call</span>(tron.led);

<span class="pl-c">// good</span>
<span class="pl-k">var</span> leds <span class="pl-k">=</span> stage.selectAll(<span class="pl-s"><span class="pl-pds">'</span>.led<span class="pl-pds">'</span></span>)
    .<span class="pl-c1">data</span>(data)
  .enter().append(<span class="pl-s"><span class="pl-pds">'</span>svg:svg<span class="pl-pds">'</span></span>)
    .class(<span class="pl-s"><span class="pl-pds">'</span>led<span class="pl-pds">'</span></span>, <span class="pl-c1">true</span>)
    .attr(<span class="pl-s"><span class="pl-pds">'</span>width<span class="pl-pds">'</span></span>,  (radius <span class="pl-k">+</span> margin) <span class="pl-k">*</span> <span class="pl-c1">2</span>)
  .append(<span class="pl-s"><span class="pl-pds">'</span>svg:g<span class="pl-pds">'</span></span>)
    .attr(<span class="pl-s"><span class="pl-pds">'</span>transform<span class="pl-pds">'</span></span>, <span class="pl-s"><span class="pl-pds">'</span>translate(<span class="pl-pds">'</span></span> <span class="pl-k">+</span> (radius <span class="pl-k">+</span> margin) <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>,<span class="pl-pds">'</span></span> <span class="pl-k">+</span> (radius <span class="pl-k">+</span> margin) <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span>)<span class="pl-pds">'</span></span>)
    .<span class="pl-c1">call</span>(tron.led);</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-逗号" class="anchor" href="#逗号" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-commas">逗号</a></h2>

<ul>
<li><p>不要将逗号放前面</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">var</span> once
  , upon
  , aTime;

<span class="pl-c">// good</span>
<span class="pl-k">var</span> once,
    upon,
    aTime;

<span class="pl-c">// bad</span>
<span class="pl-k">var</span> hero <span class="pl-k">=</span> {
    firstName<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Bob<span class="pl-pds">'</span></span>
  , lastName<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Parr<span class="pl-pds">'</span></span>
  , heroName<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Mr. Incredible<span class="pl-pds">'</span></span>
  , superPower<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>strength<span class="pl-pds">'</span></span>
};

<span class="pl-c">// good</span>
<span class="pl-k">var</span> hero <span class="pl-k">=</span> {
  firstName<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Bob<span class="pl-pds">'</span></span>,
  lastName<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Parr<span class="pl-pds">'</span></span>,
  heroName<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Mr. Incredible<span class="pl-pds">'</span></span>,
  superPower<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>strength<span class="pl-pds">'</span></span>
};</pre></div></li>
<li><p>不要加多余的逗号，这可能会在IE下引起错误，同时如果多一个逗号某些ES3的实现会计算多数组的长度。</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">var</span> hero <span class="pl-k">=</span> {
  firstName<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Kevin<span class="pl-pds">'</span></span>,
  lastName<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Flynn<span class="pl-pds">'</span></span>,
};

<span class="pl-k">var</span> heroes <span class="pl-k">=</span> [
  <span class="pl-s"><span class="pl-pds">'</span>Batman<span class="pl-pds">'</span></span>,
  <span class="pl-s"><span class="pl-pds">'</span>Superman<span class="pl-pds">'</span></span>,
];

<span class="pl-c">// good</span>
<span class="pl-k">var</span> hero <span class="pl-k">=</span> {
  firstName<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Kevin<span class="pl-pds">'</span></span>,
  lastName<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Flynn<span class="pl-pds">'</span></span>
};

<span class="pl-k">var</span> heroes <span class="pl-k">=</span> [
  <span class="pl-s"><span class="pl-pds">'</span>Batman<span class="pl-pds">'</span></span>,
  <span class="pl-s"><span class="pl-pds">'</span>Superman<span class="pl-pds">'</span></span>
];</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-分号" class="anchor" href="#分号" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-semicolons">分号</a></h2>

<ul>
<li><p>语句结束一定要加分号</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
(<span class="pl-k">function</span>() {
  <span class="pl-k">var</span> name <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>Skywalker<span class="pl-pds">'</span></span>
  <span class="pl-k">return</span> name
})()

<span class="pl-c">// good</span>
(<span class="pl-k">function</span>() {
  <span class="pl-k">var</span> name <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>Skywalker<span class="pl-pds">'</span></span>;
  <span class="pl-k">return</span> name;
})();

<span class="pl-c">// good</span>
;(<span class="pl-k">function</span>() {
  <span class="pl-k">var</span> name <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>Skywalker<span class="pl-pds">'</span></span>;
  <span class="pl-k">return</span> name;
})();</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-类型转换" class="anchor" href="#类型转换" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-type-coercion">类型转换</a></h2>

<ul>
<li>在语句的开始执行类型转换.</li>
<li><p>字符串:</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">//  =&gt; this.reviewScore = 9;</span>

<span class="pl-c">// bad</span>
<span class="pl-k">var</span> totalScore <span class="pl-k">=</span> <span class="pl-v">this</span>.reviewScore <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span><span class="pl-pds">'</span></span>;

<span class="pl-c">// good</span>
<span class="pl-k">var</span> totalScore <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span><span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-v">this</span>.reviewScore;

<span class="pl-c">// bad</span>
<span class="pl-k">var</span> totalScore <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span><span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-v">this</span>.reviewScore <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span> total score<span class="pl-pds">'</span></span>;

<span class="pl-c">// good</span>
<span class="pl-k">var</span> totalScore <span class="pl-k">=</span> <span class="pl-v">this</span>.reviewScore <span class="pl-k">+</span> <span class="pl-s"><span class="pl-pds">'</span> total score<span class="pl-pds">'</span></span>;</pre></div></li>
<li><p>对数字使用 <code>parseInt</code> 并且总是带上类型转换的基数.</p>

<div class="highlight highlight-source-js"><pre><span class="pl-k">var</span> inputValue <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>4<span class="pl-pds">'</span></span>;

<span class="pl-c">// bad</span>
<span class="pl-k">var</span> val <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">Number</span>(inputValue);

<span class="pl-c">// bad</span>
<span class="pl-k">var</span> val <span class="pl-k">=</span> <span class="pl-k">+</span>inputValue;

<span class="pl-c">// bad</span>
<span class="pl-k">var</span> val <span class="pl-k">=</span> inputValue <span class="pl-k">&gt;&gt;</span> <span class="pl-c1">0</span>;

<span class="pl-c">// bad</span>
<span class="pl-k">var</span> val <span class="pl-k">=</span> <span class="pl-c1">parseInt</span>(inputValue);

<span class="pl-c">// good</span>
<span class="pl-k">var</span> val <span class="pl-k">=</span> <span class="pl-c1">Number</span>(inputValue);

<span class="pl-c">// good</span>
<span class="pl-k">var</span> val <span class="pl-k">=</span> <span class="pl-c1">parseInt</span>(inputValue, <span class="pl-c1">10</span>);

<span class="pl-c">// good</span>
<span class="pl-c">/**</span>
<span class="pl-c"> * parseInt was the reason my code was slow.</span>
<span class="pl-c"> * Bitshifting the String to coerce it to a</span>
<span class="pl-c"> * Number made it a lot faster.</span>
<span class="pl-c"> */</span>
<span class="pl-k">var</span> val <span class="pl-k">=</span> inputValue <span class="pl-k">&gt;&gt;</span> <span class="pl-c1">0</span>;</pre></div></li>
<li><p>布尔值:</p>

<div class="highlight highlight-source-js"><pre><span class="pl-k">var</span> age <span class="pl-k">=</span> <span class="pl-c1">0</span>;

<span class="pl-c">// bad</span>
<span class="pl-k">var</span> hasAge <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">Boolean</span>(age);

<span class="pl-c">// good</span>
<span class="pl-k">var</span> hasAge <span class="pl-k">=</span> <span class="pl-c1">Boolean</span>(age);

<span class="pl-c">// good</span>
<span class="pl-k">var</span> hasAge <span class="pl-k">=</span> <span class="pl-k">!!</span>age;</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-命名约定" class="anchor" href="#命名约定" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-naming-conventions">命名约定</a></h2>

<ul>
<li><p>避免单个字符名，让你的变量名有描述意义。</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">function</span> <span class="pl-en">q</span>() {
  <span class="pl-c">// ...stuff...</span>
}

<span class="pl-c">// good</span>
<span class="pl-k">function</span> <span class="pl-en">query</span>() {
  <span class="pl-c">// ..stuff..</span>
}</pre></div></li>
<li><p>当命名对象、函数和实例时使用驼峰命名规则</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">var</span> OBJEcttsssss <span class="pl-k">=</span> {};
<span class="pl-k">var</span> this_is_my_object <span class="pl-k">=</span> {};
<span class="pl-k">var</span> <span class="pl-v">this</span><span class="pl-k">-</span>is<span class="pl-k">-</span>my<span class="pl-k">-</span>object <span class="pl-k">=</span> {};
<span class="pl-k">function</span> <span class="pl-en">c</span>() {};
<span class="pl-k">var</span> u <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">user</span>({
  name<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Bob Parr<span class="pl-pds">'</span></span>
});

<span class="pl-c">// good</span>
<span class="pl-k">var</span> thisIsMyObject <span class="pl-k">=</span> {};
<span class="pl-k">function</span> <span class="pl-en">thisIsMyFunction</span>() {};
<span class="pl-k">var</span> user <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">User</span>({
  name<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>Bob Parr<span class="pl-pds">'</span></span>
});</pre></div></li>
<li><p>当命名构造函数或类时使用驼峰式大写</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">function</span> <span class="pl-en">user</span>(<span class="pl-smi">options</span>) {
  <span class="pl-v">this</span>.<span class="pl-c1">name</span> <span class="pl-k">=</span> options.<span class="pl-c1">name</span>;
}

<span class="pl-k">var</span> bad <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">user</span>({
  name<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>nope<span class="pl-pds">'</span></span>
});

<span class="pl-c">// good</span>
<span class="pl-k">function</span> <span class="pl-en">User</span>(<span class="pl-smi">options</span>) {
  <span class="pl-v">this</span>.<span class="pl-c1">name</span> <span class="pl-k">=</span> options.<span class="pl-c1">name</span>;
}

<span class="pl-k">var</span> good <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">User</span>({
  name<span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>yup<span class="pl-pds">'</span></span>
});</pre></div></li>
<li><p>命名私有属性时前面加个下划线 <code>_</code></p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-v">this</span>.__firstName__ <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>Panda<span class="pl-pds">'</span></span>;
<span class="pl-v">this</span>.firstName_ <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>Panda<span class="pl-pds">'</span></span>;

<span class="pl-c">// good</span>
<span class="pl-v">this</span>._firstName <span class="pl-k">=</span> <span class="pl-s"><span class="pl-pds">'</span>Panda<span class="pl-pds">'</span></span>;</pre></div></li>
<li><p>当保存对 <code>this</code> 的引用时使用 <code>_this</code>.</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">function</span>() {
  <span class="pl-k">var</span> self <span class="pl-k">=</span> <span class="pl-v">this</span>;
  <span class="pl-k">return</span> <span class="pl-k">function</span>() {
    <span class="pl-en">console</span>.<span class="pl-c1">log</span>(self);
  };
}

<span class="pl-c">// bad</span>
<span class="pl-k">function</span>() {
  <span class="pl-k">var</span> that <span class="pl-k">=</span> <span class="pl-v">this</span>;
  <span class="pl-k">return</span> <span class="pl-k">function</span>() {
    <span class="pl-en">console</span>.<span class="pl-c1">log</span>(that);
  };
}

<span class="pl-c">// good</span>
<span class="pl-k">function</span>() {
  <span class="pl-k">var</span> _this <span class="pl-k">=</span> <span class="pl-v">this</span>;
  <span class="pl-k">return</span> <span class="pl-k">function</span>() {
    <span class="pl-en">console</span>.<span class="pl-c1">log</span>(_this);
  };
}</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-存取器" class="anchor" href="#存取器" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-accessors">存取器</a></h2>

<ul>
<li>属性的存取器函数不是必需的</li>
<li><p>如果你确实有存取器函数的话使用getVal() 和 setVal('hello')</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
dragon.age();

<span class="pl-c">// good</span>
dragon.getAge();

<span class="pl-c">// bad</span>
dragon.age(<span class="pl-c1">25</span>);

<span class="pl-c">// good</span>
dragon.setAge(<span class="pl-c1">25</span>);</pre></div></li>
<li><p>如果属性是布尔值，使用isVal() 或 hasVal()</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">if</span> (<span class="pl-k">!</span>dragon.age()) {
  <span class="pl-k">return</span> <span class="pl-c1">false</span>;
}

<span class="pl-c">// good</span>
<span class="pl-k">if</span> (<span class="pl-k">!</span>dragon.hasAge()) {
  <span class="pl-k">return</span> <span class="pl-c1">false</span>;
}</pre></div></li>
<li><p>可以创建get()和set()函数，但是要保持一致</p>

<div class="highlight highlight-source-js"><pre><span class="pl-k">function</span> <span class="pl-en">Jedi</span>(<span class="pl-smi">options</span>) {
  options <span class="pl-k">||</span> (options <span class="pl-k">=</span> {});
  <span class="pl-k">var</span> lightsaber <span class="pl-k">=</span> options.lightsaber <span class="pl-k">||</span> <span class="pl-s"><span class="pl-pds">'</span>blue<span class="pl-pds">'</span></span>;
  <span class="pl-v">this</span>.set(<span class="pl-s"><span class="pl-pds">'</span>lightsaber<span class="pl-pds">'</span></span>, lightsaber);
}

<span class="pl-c1">Jedi</span>.<span class="pl-c1">prototype</span>.<span class="pl-en">set</span> <span class="pl-k">=</span> <span class="pl-k">function</span>(<span class="pl-smi">key</span>, <span class="pl-smi">val</span>) {
  <span class="pl-v">this</span>[key] <span class="pl-k">=</span> val;
};

<span class="pl-c1">Jedi</span>.<span class="pl-c1">prototype</span>.<span class="pl-en">get</span> <span class="pl-k">=</span> <span class="pl-k">function</span>(<span class="pl-smi">key</span>) {
  <span class="pl-k">return</span> <span class="pl-v">this</span>[key];
};</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-构造器" class="anchor" href="#构造器" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-constructors">构造器</a></h2>

<ul>
<li><p>给对象原型分配方法，而不是用一个新的对象覆盖原型，覆盖原型会使继承出现问题。</p>

<div class="highlight highlight-source-js"><pre><span class="pl-k">function</span> <span class="pl-en">Jedi</span>() {
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>new jedi<span class="pl-pds">'</span></span>);
}

<span class="pl-c">// bad</span>
<span class="pl-c1">Jedi</span>.<span class="pl-c1">prototype</span> <span class="pl-k">=</span> {
  <span class="pl-en">fight</span><span class="pl-k">:</span> <span class="pl-k">function</span> <span class="pl-en">fight</span>() {
    <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>fighting<span class="pl-pds">'</span></span>);
  },

  <span class="pl-en">block</span><span class="pl-k">:</span> <span class="pl-k">function</span> <span class="pl-en">block</span>() {
    <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>blocking<span class="pl-pds">'</span></span>);
  }
};

<span class="pl-c">// good</span>
<span class="pl-c1">Jedi</span>.<span class="pl-c1">prototype</span>.<span class="pl-en">fight</span> <span class="pl-k">=</span> <span class="pl-k">function</span> <span class="pl-en">fight</span>() {
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>fighting<span class="pl-pds">'</span></span>);
};

<span class="pl-c1">Jedi</span>.<span class="pl-c1">prototype</span>.<span class="pl-en">block</span> <span class="pl-k">=</span> <span class="pl-k">function</span> <span class="pl-en">block</span>() {
  <span class="pl-en">console</span>.<span class="pl-c1">log</span>(<span class="pl-s"><span class="pl-pds">'</span>blocking<span class="pl-pds">'</span></span>);
};</pre></div></li>
<li><p>方法可以返回 <code>this</code> 帮助方法可链。</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-c1">Jedi</span>.<span class="pl-c1">prototype</span>.<span class="pl-en">jump</span> <span class="pl-k">=</span> <span class="pl-k">function</span>() {
  <span class="pl-v">this</span>.jumping <span class="pl-k">=</span> <span class="pl-c1">true</span>;
  <span class="pl-k">return</span> <span class="pl-c1">true</span>;
};

<span class="pl-c1">Jedi</span>.<span class="pl-c1">prototype</span>.<span class="pl-en">setHeight</span> <span class="pl-k">=</span> <span class="pl-k">function</span>(<span class="pl-smi">height</span>) {
  <span class="pl-v">this</span>.<span class="pl-c1">height</span> <span class="pl-k">=</span> height;
};

<span class="pl-k">var</span> luke <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">Jedi</span>();
luke.jump(); <span class="pl-c">// =&gt; true</span>
luke.setHeight(<span class="pl-c1">20</span>) <span class="pl-c">// =&gt; undefined</span>

<span class="pl-c">// good</span>
<span class="pl-c1">Jedi</span>.<span class="pl-c1">prototype</span>.<span class="pl-en">jump</span> <span class="pl-k">=</span> <span class="pl-k">function</span>() {
  <span class="pl-v">this</span>.jumping <span class="pl-k">=</span> <span class="pl-c1">true</span>;
  <span class="pl-k">return</span> <span class="pl-v">this</span>;
};

<span class="pl-c1">Jedi</span>.<span class="pl-c1">prototype</span>.<span class="pl-en">setHeight</span> <span class="pl-k">=</span> <span class="pl-k">function</span>(<span class="pl-smi">height</span>) {
  <span class="pl-v">this</span>.<span class="pl-c1">height</span> <span class="pl-k">=</span> height;
  <span class="pl-k">return</span> <span class="pl-v">this</span>;
};

<span class="pl-k">var</span> luke <span class="pl-k">=</span> <span class="pl-k">new</span> <span class="pl-en">Jedi</span>();

luke.jump()
  .setHeight(<span class="pl-c1">20</span>);</pre></div></li>
<li><p>可以写一个自定义的toString()方法，但是确保它工作正常并且不会有副作用。</p>

<div class="highlight highlight-source-js"><pre><span class="pl-k">function</span> <span class="pl-en">Jedi</span>(<span class="pl-smi">options</span>) {
  options <span class="pl-k">||</span> (options <span class="pl-k">=</span> {});
  <span class="pl-v">this</span>.<span class="pl-c1">name</span> <span class="pl-k">=</span> options.<span class="pl-c1">name</span> <span class="pl-k">||</span> <span class="pl-s"><span class="pl-pds">'</span>no name<span class="pl-pds">'</span></span>;
}

<span class="pl-c1">Jedi</span>.<span class="pl-c1">prototype</span>.<span class="pl-en">getName</span> <span class="pl-k">=</span> <span class="pl-k">function</span> <span class="pl-en">getName</span>() {
  <span class="pl-k">return</span> <span class="pl-v">this</span>.<span class="pl-c1">name</span>;
};

<span class="pl-c1">Jedi</span>.<span class="pl-c1">prototype</span>.<span class="pl-en">toString</span> <span class="pl-k">=</span> <span class="pl-k">function</span> <span class="pl-en">toString</span>() {
  <span class="pl-k">return</span> <span class="pl-s"><span class="pl-pds">'</span>Jedi - <span class="pl-pds">'</span></span> <span class="pl-k">+</span> <span class="pl-v">this</span>.getName();
};</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-事件" class="anchor" href="#事件" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-events">事件</a></h2>

<ul>
<li><p>当给事件附加数据时，传入一个哈希而不是原始值，这可以让后面的贡献者加入更多数据到事件数据里而不用找出并更新那个事件的事件处理器</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
$(<span class="pl-v">this</span>).trigger(<span class="pl-s"><span class="pl-pds">'</span>listingUpdated<span class="pl-pds">'</span></span>, listing.<span class="pl-c1">id</span>);

...

$(<span class="pl-v">this</span>).on(<span class="pl-s"><span class="pl-pds">'</span>listingUpdated<span class="pl-pds">'</span></span>, <span class="pl-k">function</span>(<span class="pl-smi">e</span>, <span class="pl-smi">listingId</span>) {
  <span class="pl-c">// do something with listingId</span>
});</pre></div>

<p>更好:</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// good</span>
$(<span class="pl-v">this</span>).trigger(<span class="pl-s"><span class="pl-pds">'</span>listingUpdated<span class="pl-pds">'</span></span>, { listingId <span class="pl-k">:</span> listing.<span class="pl-c1">id</span> });

...

$(<span class="pl-v">this</span>).on(<span class="pl-s"><span class="pl-pds">'</span>listingUpdated<span class="pl-pds">'</span></span>, <span class="pl-k">function</span>(<span class="pl-smi">e</span>, <span class="pl-smi">data</span>) {
  <span class="pl-c">// do something with data.listingId</span>
});</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-模块" class="anchor" href="#模块" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-modules">模块</a></h2>

<ul>
<li>模块应该以 <code>!</code> 开始，这保证了如果一个有问题的模块忘记包含最后的分号在合并后不会出现错误</li>
<li>这个文件应该以驼峰命名，并在同名文件夹下，同时导出的时候名字一致</li>
<li>加入一个名为noConflict()的方法来设置导出的模块为之前的版本并返回它</li>
<li><p>总是在模块顶部声明 <code>'use strict';</code></p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// fancyInput/fancyInput.js</span>

<span class="pl-k">!</span><span class="pl-k">function</span>(<span class="pl-smi">global</span>) {
  <span class="pl-s"><span class="pl-pds">'</span>use strict<span class="pl-pds">'</span></span>;

  <span class="pl-k">var</span> previousFancyInput <span class="pl-k">=</span> <span class="pl-c1">global</span>.FancyInput;

  <span class="pl-k">function</span> <span class="pl-en">FancyInput</span>(<span class="pl-smi">options</span>) {
    <span class="pl-v">this</span>.<span class="pl-c1">options</span> <span class="pl-k">=</span> options <span class="pl-k">||</span> {};
  }

  <span class="pl-c1">FancyInput</span>.<span class="pl-en">noConflict</span> <span class="pl-k">=</span> <span class="pl-k">function</span> <span class="pl-en">noConflict</span>() {
    <span class="pl-c1">global</span>.FancyInput <span class="pl-k">=</span> previousFancyInput;
    <span class="pl-k">return</span> FancyInput;
  };

  <span class="pl-c1">global</span>.FancyInput <span class="pl-k">=</span> FancyInput;
}(<span class="pl-v">this</span>);</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-jquery" class="anchor" href="#jquery" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-jquery">jQuery</a></h2>

<ul>
<li><p>缓存jQuery查询</p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
<span class="pl-k">function</span> <span class="pl-en">setSidebar</span>() {
  $(<span class="pl-s"><span class="pl-pds">'</span>.sidebar<span class="pl-pds">'</span></span>).hide();

  <span class="pl-c">// ...stuff...</span>

  $(<span class="pl-s"><span class="pl-pds">'</span>.sidebar<span class="pl-pds">'</span></span>).css({
    <span class="pl-s"><span class="pl-pds">'</span>background-color<span class="pl-pds">'</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>pink<span class="pl-pds">'</span></span>
  });
}

<span class="pl-c">// good</span>
<span class="pl-k">function</span> <span class="pl-en">setSidebar</span>() {
  <span class="pl-k">var</span> $sidebar <span class="pl-k">=</span> $(<span class="pl-s"><span class="pl-pds">'</span>.sidebar<span class="pl-pds">'</span></span>);
  $sidebar.hide();

  <span class="pl-c">// ...stuff...</span>

  $sidebar.css({
    <span class="pl-s"><span class="pl-pds">'</span>background-color<span class="pl-pds">'</span></span><span class="pl-k">:</span> <span class="pl-s"><span class="pl-pds">'</span>pink<span class="pl-pds">'</span></span>
  });
}</pre></div></li>
<li><p>对DOM查询使用级联的 <code>$('.sidebar ul')</code> 或 <code>$('.sidebar ul')</code>，<a href="http://jsperf.com/jquery-find-vs-context-sel/16">jsPerf</a></p></li>
<li><p>对有作用域的jQuery对象查询使用 <code>find</code></p>

<div class="highlight highlight-source-js"><pre><span class="pl-c">// bad</span>
$(<span class="pl-s"><span class="pl-pds">'</span>.sidebar<span class="pl-pds">'</span></span>, <span class="pl-s"><span class="pl-pds">'</span>ul<span class="pl-pds">'</span></span>).hide();

<span class="pl-c">// bad</span>
$(<span class="pl-s"><span class="pl-pds">'</span>.sidebar<span class="pl-pds">'</span></span>).<span class="pl-c1">find</span>(<span class="pl-s"><span class="pl-pds">'</span>ul<span class="pl-pds">'</span></span>).hide();

<span class="pl-c">// good</span>
$(<span class="pl-s"><span class="pl-pds">'</span>.sidebar ul<span class="pl-pds">'</span></span>).hide();

<span class="pl-c">// good</span>
$(<span class="pl-s"><span class="pl-pds">'</span>.sidebar &gt; ul<span class="pl-pds">'</span></span>).hide();

<span class="pl-c">// good (slower)</span>
$sidebar.<span class="pl-c1">find</span>(<span class="pl-s"><span class="pl-pds">'</span>ul<span class="pl-pds">'</span></span>);

<span class="pl-c">// good (faster)</span>
$($sidebar[<span class="pl-c1">0</span>]).<span class="pl-c1">find</span>(<span class="pl-s"><span class="pl-pds">'</span>ul<span class="pl-pds">'</span></span>);</pre></div>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-ecmascript-5兼容性" class="anchor" href="#ecmascript-5兼容性" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-es5">ECMAScript 5兼容性</a></h2>

<ul>
<li><p>参考<a href="https://twitter.com/kangax/">Kangax</a>的 ES5 <a href="http://kangax.github.com/es5-compat-table/">compatibility table</a></p>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-性能" class="anchor" href="#性能" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-performance">性能</a></h2>

<ul>
<li><a href="http://kellegous.com/j/2013/01/26/layout-performance/">On Layout &amp; Web Performance</a></li>
<li><a href="http://jsperf.com/string-vs-array-concat/2">String vs Array Concat</a></li>
<li><a href="http://jsperf.com/try-catch-in-loop-cost">Try/Catch Cost In a Loop</a></li>
<li><a href="http://jsperf.com/bang-function">Bang Function</a></li>
<li><a href="http://jsperf.com/jquery-find-vs-context-sel/13">jQuery Find vs Context, Selector</a></li>
<li><a href="http://jsperf.com/innerhtml-vs-textcontent-for-script-text">innerHTML vs textContent for script text</a></li>
<li><a href="http://jsperf.com/ya-string-concat">Long String Concatenation</a></li>
<li><p>Loading...</p>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-资源" class="anchor" href="#资源" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-resources">资源</a></h2>

<p><strong>Read This</strong></p>

<ul>
<li><a href="http://es5.github.com/">Annotated ECMAScript 5.1</a></li>
</ul>

<p><strong>其它规范</strong></p>

<ul>
<li><a href="http://google-styleguide.googlecode.com/svn/trunk/javascriptguide.xml">Google JavaScript Style Guide</a></li>
<li><a href="http://docs.jquery.com/JQuery_Core_Style_Guidelines">jQuery Core Style Guidelines</a></li>
<li><a href="https://github.com/rwldrn/idiomatic.js/">Principles of Writing Consistent, Idiomatic JavaScript</a></li>
</ul>

<p><strong>其它风格</strong></p>

<ul>
<li><a href="https://gist.github.com/4135065">Naming this in nested functions</a> - Christian Johansen</li>
<li><a href="https://github.com/airbnb/javascript/issues/52">Conditional Callbacks</a></li>
</ul>

<p><strong>阅读更多</strong></p>

<ul>
<li><a href="http://javascriptweblog.wordpress.com/2010/10/25/understanding-javascript-closures/">Understanding JavaScript Closures</a> - Angus Croll</li>
</ul>

<p><strong>书籍</strong></p>

<ul>
<li><a href="http://www.amazon.com/JavaScript-Good-Parts-Douglas-Crockford/dp/0596517742">JavaScript: The Good Parts</a> - Douglas Crockford</li>
<li><a href="http://www.amazon.com/JavaScript-Patterns-Stoyan-Stefanov/dp/0596806752">JavaScript Patterns</a> - Stoyan Stefanov</li>
<li><a href="http://www.amazon.com/JavaScript-Design-Patterns-Recipes-Problem-Solution/dp/159059908X">Pro JavaScript Design Patterns</a>  - Ross Harmes and Dustin Diaz</li>
<li><a href="http://www.amazon.com/High-Performance-Web-Sites-Essential/dp/0596529309">High Performance Web Sites: Essential Knowledge for Front-End Engineers</a> - Steve Souders</li>
<li><a href="http://www.amazon.com/Maintainable-JavaScript-Nicholas-C-Zakas/dp/1449327680">Maintainable JavaScript</a> - Nicholas C. Zakas</li>
<li><a href="http://www.amazon.com/JavaScript-Web-Applications-Alex-MacCaw/dp/144930351X">JavaScript Web Applications</a> - Alex MacCaw</li>
<li><a href="http://www.amazon.com/Pro-JavaScript-Techniques-John-Resig/dp/1590597273">Pro JavaScript Techniques</a> - John Resig</li>
<li><a href="http://www.amazon.com/Smashing-Node-js-JavaScript-Everywhere-Magazine/dp/1119962595">Smashing Node.js: JavaScript Everywhere</a> - Guillermo Rauch</li>
</ul>

<p><strong>博客</strong></p>

<ul>
<li><a href="http://adamlu.com/">Adam Lu</a></li>
<li><a href="http://dailyjs.com/">DailyJS</a></li>
<li><a href="http://javascriptweekly.com/">JavaScript Weekly</a></li>
<li><a href="http://javascriptweblog.wordpress.com/">JavaScript, JavaScript...</a></li>
<li><a href="http://weblog.bocoup.com/">Bocoup Weblog</a></li>
<li><a href="http://www.adequatelygood.com/">Adequately Good</a></li>
<li><a href="http://www.nczonline.net/">NCZOnline</a></li>
<li><a href="http://perfectionkills.com/">Perfection Kills</a></li>
<li><a href="http://benalman.com/">Ben Alman</a></li>
<li><a href="http://dmitry.baranovskiy.com/">Dmitry Baranovskiy</a></li>
<li><a href="http://dustindiaz.com/">Dustin Diaz</a></li>
<li><p><a href="http://net.tutsplus.com/?s=javascript">nettuts</a></p>

<p><strong><a href="#TOC">[⬆]</a></strong></p></li>
</ul>

<h2><a id="user-content-哪些人在使用" class="anchor" href="#哪些人在使用" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-in-the-wild">哪些人在使用</a></h2>

<p>这是一些使用这个风格规范的组织，给我们发pull request或打开一个问题，我们会把你加到列表中。</p>

<ul>
<li><strong>Airbnb</strong>: <a href="https://github.com/airbnb/javascript">airbnb/javascript</a></li>
<li><strong>American Insitutes for Research</strong>: <a href="https://github.com/AIRAST/javascript">AIRAST/javascript</a></li>
<li><strong>ExactTarget</strong>: <a href="https://github.com/ExactTarget/javascript">ExactTarget/javascript</a></li>
<li><strong>GeneralElectric</strong>: <a href="https://github.com/GeneralElectric/javascript">GeneralElectric/javascript</a></li>
<li><strong>GoodData</strong>: <a href="https://github.com/gooddata/gdc-js-style">gooddata/gdc-js-style</a></li>
<li><strong>How About We</strong>: <a href="https://github.com/howaboutwe/javascript">howaboutwe/javascript</a></li>
<li><strong>MinnPost</strong>: <a href="https://github.com/MinnPost/javascript">MinnPost/javascript</a></li>
<li><strong>ModCloth</strong>: <a href="https://github.com/modcloth/javascript">modcloth/javascript</a></li>
<li><strong>National Geographic</strong>: <a href="https://github.com/natgeo/javascript">natgeo/javascript</a></li>
<li><strong>National Park Service</strong>: <a href="https://github.com/nationalparkservice/javascript">nationalparkservice/javascript</a></li>
<li><strong>Razorfish</strong>: <a href="https://github.com/razorfish/javascript-style-guide">razorfish/javascript-style-guide</a></li>
<li><strong>Shutterfly</strong>: <a href="https://github.com/shutterfly/javascript">shutterfly/javascript</a></li>
<li><strong>Userify</strong>: <a href="https://github.com/userify/javascript">userify/javascript</a></li>
<li><strong>Zillow</strong>: <a href="https://github.com/zillow/javascript">zillow/javascript</a></li>
<li><strong>ZocDoc</strong>: <a href="https://github.com/ZocDoc/javascript">ZocDoc/javascript</a></li>
</ul>

<h2><a id="user-content-翻译" class="anchor" href="#翻译" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-translation">翻译</a></h2>

<p>这个风格规范也有其它语言版本：</p>

<ul>
<li><img class="emoji" title=":de:" alt=":de:" src="https://assets-cdn.github.com/images/icons/emoji/unicode/1f1e9-1f1ea.png" height="20" width="20" align="absmiddle"> <strong>German</strong>: <a href="https://github.com/timofurrer/javascript-style-guide">timofurrer/javascript-style-guide</a></li>
<li><img class="emoji" title=":jp:" alt=":jp:" src="https://assets-cdn.github.com/images/icons/emoji/unicode/1f1ef-1f1f5.png" height="20" width="20" align="absmiddle"> <strong>Japanese</strong>: <a href="https://github.com/mitsuruog/javacript-style-guide">mitsuruog/javacript-style-guide</a></li>
<li>:br: <strong>Portuguese</strong>: <a href="https://github.com/armoucar/javascript-style-guide">armoucar/javascript-style-guide</a></li>
<li><img class="emoji" title=":cn:" alt=":cn:" src="https://assets-cdn.github.com/images/icons/emoji/unicode/1f1e8-1f1f3.png" height="20" width="20" align="absmiddle"> <strong>Chinese</strong>: <a href="https://github.com/adamlu/javascript-style-guide">adamlu/javascript-style-guide</a></li>
</ul>

<h2><a id="user-content-javascript风格指南" class="anchor" href="#javascript风格指南" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-guide-guide">JavaScript风格指南</a></h2>

<ul>
<li><a href="https://github.com/airbnb/javascript/wiki/The-JavaScript-Style-Guide-Guide">Reference</a></li>
</ul>

<h2><a id="user-content-贡献者" class="anchor" href="#贡献者" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-authors">贡献者</a></h2>

<ul>
<li><a href="https://github.com/airbnb/javascript/graphs/contributors">View Contributors</a></li>
</ul>

<h2><a id="user-content-许可" class="anchor" href="#许可" aria-hidden="true"><span class="octicon octicon-link"></span></a><a name="user-content-license">许可</a></h2>

<p>(The MIT License)</p>

<p>Copyright (c) 2012 Airbnb</p>

<p>Permission is hereby granted, free of charge, to any person obtaining
a copy of this software and associated documentation files (the
'Software'), to deal in the Software without restriction, including
without limitation the rights to use, copy, modify, merge, publish,
distribute, sublicense, and/or sell copies of the Software, and to
permit persons to whom the Software is furnished to do so, subject to
the following conditions:</p>

<p>The above copyright notice and this permission notice shall be
included in all copies or substantial portions of the Software.</p>

<p>THE SOFTWARE IS PROVIDED 'AS IS', WITHOUT WARRANTY OF ANY KIND,
EXPRESS OR IMPLIED, INCLUDING BUT NOT LIMITED TO THE WARRANTIES OF
MERCHANTABILITY, FITNESS FOR A PARTICULAR PURPOSE AND NONINFRINGEMENT.
IN NO EVENT SHALL THE AUTHORS OR COPYRIGHT HOLDERS BE LIABLE FOR ANY
CLAIM, DAMAGES OR OTHER LIABILITY, WHETHER IN AN ACTION OF CONTRACT,
TORT OR OTHERWISE, ARISING FROM, OUT OF OR IN CONNECTION WITH THE
SOFTWARE OR THE USE OR OTHER DEALINGS IN THE SOFTWARE.</p>

<p><strong><a href="#TOC">[⬆]</a></strong></p>

<h1><a id="" class="anchor" href="#" aria-hidden="true"><span class="octicon octicon-link"></span></a>};</h1>
</article>
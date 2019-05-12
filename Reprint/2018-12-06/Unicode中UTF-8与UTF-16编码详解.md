---
title: 'Unicode中UTF-8与UTF-16编码详解' 
date: 2018-12-06 2:30:09
hidden: true
slug: glj6lxtvthv
categories: [reprint]
---

{{< raw >}}

                    
<h1 id="articleHeader0">概述</h1>
<p>本文通过介绍Unicode编码以及对应的两种编码方式UTF-8和UTF-16，让读者能够了解关于字符串编码的相关知识，同时能够弄清楚Unicode和UTF-8和UTF-16之间的关系。</p>
<p>本文的主要内容为：</p>
<ul>
<li>Unicode编码，包含Unicode编码基础知识以及与UTF-8和UTF-16这两种编码方式的关系</li>
<li>UTF-8编码，包含基础概念和Unicode编码转换到UTF-8编码方式</li>
<li>UTF-16编码，包含基础概念和Unicode编码转换到UTF-16编码方式</li>
<li>JavaScript中string与DOMString</li>
</ul>
<p>本文作为<a href="https://github.com/dcodeIO/utfx" rel="nofollow noreferrer" target="_blank">utfx.js</a>源码解析的基础知识储备文章，通过了解UTF-8和UTF-16这两种编码方式，读者能够理解使用JavaScript进行编码转换的原理。</p>
<p>如果想了解编码转换的使用场景，可以阅读我之前的博客<a href="https://juejin.im/post/5abdc38ef265da2375070008" rel="nofollow noreferrer" target="_blank">WebSocket系列之JavaScript字符串如何与二进制数据间进行互相转换</a>。</p>
<p>如果想了解<a href="https://github.com/dcodeIO/utfx" rel="nofollow noreferrer" target="_blank">utfx.js</a>相关的源码内容，可以关注我的后续文章。</p>
<h1 id="articleHeader1">Unicode编码</h1>
<h2 id="articleHeader2">概念</h2>
<blockquote>Unicode（<a href="https://baike.baidu.com/item/%E7%BB%9F%E4%B8%80%E7%A0%81" rel="nofollow noreferrer" target="_blank">统一码</a>、万国码、单一码）是计算机科学领域里的一项业界标准,包括字符集、编码方案等。Unicode 是为了解决传统的字符编码方案的局限而产生的，它为每种语言中的每个字符设定了统一并且唯一的<a href="https://baike.baidu.com/item/%E4%BA%8C%E8%BF%9B%E5%88%B6" rel="nofollow noreferrer" target="_blank">二进制</a>编码，以满足跨语言、跨平台进行文本转换、处理的要求。1990年开始研发，1994年正式公布。</blockquote>
<p>通常Unicode编码是通过2 Byte来表示一个字符的，如<code>U+A12B</code>，2 Byte的二进制表示方法结果就是<code>1010(A)0001(1) 0010(2)1011(B)</code>。</p>
<p>简单介绍完了Unicode，我们来看下UTF-8和UTF-16。需要注意的是：<strong>UTF是Unicode TransferFormat的缩写，UTF-8和UTF-16都是把Unicode码转换成程序数据的一种编码方式。</strong></p>
<h1 id="articleHeader3">UTF-8</h1>
<h2 id="articleHeader4">概念</h2>
<blockquote>UTF-8（8-bit Unicode Transformation Format）是一种针对Unicode的可变长度字符编码，又称万国码。由Ken Thompson于1992年创建。现在已经标准化为RFC 3629。UTF-8用1到6个字节编码Unicode字符。用在网页上可以统一页面显示中文简体繁体及其它语言（如英文，日文，韩文）。</blockquote>
<p>通过上面的介绍我们可以知道，UTF-8是一种非常通用的<strong>可变长</strong>字符编码方式。</p>
<p>首先，我们来介绍下什么叫做<strong>可变长</strong>编码？可变长编码就是指在针对某个字符进行编码时，他的表示长度是不固定的。像UTF-8里面，ASCII所表示的字符集就是用1 Byte来表示，而大部分汉字则是用3 Byte来表示。</p>
<p>相较于Unicode统一使用2 Byte来表示字符，在遇到大部分字符都可以用1 Byte表示时，能够节省许多存储空间。但是，如果遇到需要用超过2 Byte来表示的字符，那么UTF-8的编码方式则会消耗更多的存储空间。</p>
<h2 id="articleHeader5">表示方式</h2>
<p>通过上面的介绍我们可以知道，不同的Unicode码在UTF-8中占用了不同的存储空间。下面我们就通过一个表格来看下将Unicode字符转换为UTF-8编码方式的具体步骤。其中的<code>?</code>表示转换成UTF-8编码后，Unicode码占用的二进制位置。</p>
<table>
<thead><tr>
<th>Unicode码范围</th>
<th>UTF-8编码方式</th>
</tr></thead>
<tbody>
<tr>
<td>
<code>U+0000</code>~<code>U+007F</code>
</td>
<td>0????????</td>
</tr>
<tr>
<td>
<code>U+0080</code>~<code>U+07FF</code>
</td>
<td>110????? 10??????</td>
</tr>
<tr>
<td>
<code>U+0800</code>~<code>U+FFFF</code>
</td>
<td>1110???? 10?????? 10??????</td>
</tr>
<tr>
<td>
<code>U+10000</code>~<code>U+10FFFF</code>
</td>
<td>11110??? 10?????? 10?????? 10??????</td>
</tr>
</tbody>
</table>
<p>当我们得到Unicode码后，我们先根据上面的这个表判断其所处的范围，然后将Unicode码转换为二进制表示，从后往前截取UTF-8编码中所留为之长度，从前往后依次填入对应位置，所即可得到UTF-8的编码。我们举两个例子来看下：</p>
<ul>
<li>
<code>U+0020</code>，这个字符的小于0000 007F，所以只需要用1 Byte来进行编码。<code>U+0020</code>的二进制表示为<code>0000(0)0000(0) 0010(2)0000(0)</code>，那么从后往前截取7位得到<code>010 0000</code>，放入UTF-8编码方式中，得到的结果为<code>00101111</code>，转换为十六进制得到<code>2F</code>。因此存储在内存中的的顺序就是<code>2F</code>。</li>
<li>
<code>U+A12B</code>，这个字符大于0000 0800，小于0000 FFFF，因此需要用3 Byte来进行编码。<code>U+A12B</code>的二进制表示为<code>1010(A)0001(1) 0010(2)1011(B)</code>。，那么从后往前截取16位得到<code>10100001 00101011</code>（Unicode码本身），放入UTF-8编码中，得到的结果为<code>11101010 10000100 10101011</code>，转换十六进制得到<code>EA84AB</code>。因此，存储在内存中的顺序就是<code>EA 84 AB</code>。</li>
</ul>
<p>通过上面的例子，我相信大家对UTF-8的编码有了一个深入的理解。下面，让我们来看下另一种编码方式——UTF-16。</p>
<h1 id="articleHeader6">UTF-16</h1>
<h2 id="articleHeader7">概念</h2>
<blockquote>UTF-16是<a href="https://baike.baidu.com/item/Unicode" rel="nofollow noreferrer" target="_blank">Unicode</a>字符编码五层次模型的第三层：字符编码表（Character Encoding Form，也称为 "storage format"）的一种实现方式。即把Unicode字符集的抽象码位映射为16位长的整数（即码元， 长度为2 Byte）的序列，用于数据存储或传递。Unicode字符的码位，需要1个或者2个16位长的码元来表示，因此这是一个变长表示。</blockquote>
<p>引用维基百科中对于UTF-16编码的解释我们可以知道，UTF-16最少也会用2 Byte来表示一个字符，因此没有办法兼容ASCII编码（ASCII编码使用1 Byte来进行存储）。</p>
<h2 id="articleHeader8">表示方式</h2>
<p>在UTF-16中，我们将Unicode分为了两个范围，分别通过不同的方式进行存储。具体表示见下图。</p>
<table>
<thead><tr>
<th>Unicode范围</th>
<th>UTF-16编码方式</th>
</tr></thead>
<tbody>
<tr>
<td>
<code>U+000</code>~<code>U+FFFF</code>
</td>
<td>2 Byte存储，编码后等于Unicode值</td>
</tr>
<tr>
<td>
<code>U+10000</code>~<code>U+10FFFF </code>
</td>
<td>4 Byte存储，现将Unicode值减去（0x10000），得到20bit长的值。再将Unicode分为高10位和低10位。UTF-16编码的高位是2 Byte，高10位Unicode范围为<code>0</code>-<code>0x3FF</code>，将Unicode值加上<code>0XD800</code>，得到高位代理（或称为前导代理，存储高位）；低位也是2 Byte，低十位Unicode范围一样为<code>0</code>~<code>0x3FF</code>，将Unicode值加上<code>0xDC00</code>,得到低位代理（或称为后尾代理，存储低位）</td>
</tr>
</tbody>
</table>
<p>根据上面的转换方式，我们就能够将Unicode码根据UTF-16的编码方式进行转换。下面我们仍然通过两个例子来看下：</p>
<ul>
<li>
<code>U+0020</code>，这个值的范围在第一部分，即经过UTF-16编码后，结果仍然为<code>U+0020</code>，在内存中的顺序为<code>00 20</code>。</li>
<li>
<code>U+12345</code>, 这个值的范围在第二部分，因此需要先减去<code>0x10000</code>，得到<code>0x02345</code>，拆分成高10位<code>00 0000 1000</code>和低10位<code>11 0100 0101</code>。根据上面规则加上特定值后，高位代理值为<code>D808</code>，低位代理值为<code>DF45</code>，最终内存中的顺序为<code>D8 08 DF 45</code>。</li>
</ul>
<h1 id="articleHeader9">JavaScript中的string与DOMString</h1>
<p>在JavaScript中，所有的string类型（或者被称为<a href="https://developer.mozilla.org/zh-CN/docs/Web/API/DOMString" rel="nofollow noreferrer" target="_blank">DOMString</a>）都是使用UTF-16编码的。</p>
<p>因此，当我们需要转换成二进制与后端进行通信时，需要注意相关的编码方式。</p>
<h1 id="articleHeader10">总结</h1>
<p>本文通过对Unicode编码和UTF-8和UTF-16两种编码方式进行介绍，让大家了解Unicode编码以及相关的两种程序数据编码方式。</p>
<p>本文是作为<a href="https://github.com/dcodeIO/utfx" rel="nofollow noreferrer" target="_blank">utfx.js</a>源码分析的基础知识储备文章，在稍后的时间将会给大家带来相关内容的后续文章——utfx.js源码解析，让大家能够了解在JavaScript中如何进行相关的编码转换。</p>

                
{{< /raw >}}

# 版权声明
本文资源来源互联网，仅供学习研究使用，版权归该资源的合法拥有者所有，

本文仅用于学习、研究和交流目的。转载请注明出处、完整链接以及原作者。

原作者若认为本站侵犯了您的版权，请联系我们，我们会立即删除！

## 原文标题
Unicode中UTF-8与UTF-16编码详解

## 原文链接
[https://segmentfault.com/a/1190000014324711](https://segmentfault.com/a/1190000014324711)


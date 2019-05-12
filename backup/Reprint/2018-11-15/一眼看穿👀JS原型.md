---
title: '一眼看穿👀JS原型' 
date: 2018-11-15 21:20:48
hidden: true
slug: rvy4d46eobd
categories: [reprint]
---

{{< raw >}}
<h2>&#x539F;&#x578B;</h2><p>&#x539F;&#x578B;&#x8FD8;&#x662F;&#x6BD4;&#x8F83;&#x91CD;&#x8981;&#x7684;&#xFF0C;&#x60F3;&#x5355;&#x72EC;&#x62BD;&#x51FA;&#x4E00;&#x7AE0;&#x6765;&#x7EC6;&#x8BF4;&#xFF0C;&#x8BF4;&#x5230;&#x539F;&#x578B;&#xFF0C;&#x90A3;&#x4E48;&#x4EC0;&#x4E48;&#x662F;&#x539F;&#x578B;&#x5462;&#xFF1F;</p><blockquote>&#x5728;&#x6784;&#x9020;&#x51FD;&#x6570;&#x521B;&#x5EFA;&#x51FA;&#x6765;&#x7684;&#x65F6;&#x5019;&#xFF0C;&#x90FD;&#x6709;&#x4E00;&#x4E2A;prototype(&#x539F;&#x578B;)&#x5C5E;&#x6027;&#xFF0C;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#x662F;&#x4E00;&#x4E2A;&#x6307;&#x9488;&#xFF0C;&#x7CFB;&#x7EDF;&#x4F1A;&#x9ED8;&#x8BA4;&#x7684;&#x521B;&#x5EFA;&#x5E76;&#x5173;&#x8054;&#x4E00;&#x4E2A;&#x5BF9;&#x8C61;&#xFF0C;&#x8FD9;&#x4E2A;&#x5BF9;&#x8C61;&#x5C31;&#x662F;&#x539F;&#x578B;&#xFF0C;&#x539F;&#x578B;&#x5BF9;&#x8C61;&#x9ED8;&#x8BA4;&#x662F;&#x7A7A;&#x5BF9;&#x8C61;&#xFF0C;&#x800C;&#x8FD9;&#x4E2A;&#x5BF9;&#x8C61;&#x7684;&#x7528;&#x9014;&#x662F;&#x5305;&#x542B;&#x53EF;&#x4EE5;&#x7531;&#x7279;&#x5B9A;&#x7C7B;&#x578B;&#x7684;&#x6240;&#x6709;&#x5B9E;&#x4F8B;&#x5171;&#x4EAB;&#x7684;&#x5C5E;&#x6027;&#x548C;&#x65B9;&#x6CD5;&#x3002;<br>&#x8BF4;&#x767D;&#x4E86;&#x5C31;&#x662F;&#x53EF;&#x4EE5;&#x5728;&#x6784;&#x9020;&#x51FD;&#x6570;&#x4E0A;&#x8C03;&#x7528;prototype&#x5C5E;&#x6027;&#x6765;&#x6307;&#x5411;&#x539F;&#x578B;&#xFF0C;&#x4ECE;&#x800C;&#x521B;&#x5EFA;&#x90A3;&#x4E2A;&#x5BF9;&#x8C61;&#x5B9E;&#x4F8B;&#x7684;&#x539F;&#x578B;&#x5BF9;&#x8C61;</blockquote><p>&#x4F7F;&#x7528;&#x539F;&#x578B;&#x6709;&#x4EC0;&#x4E48;&#x597D;&#x5904;&#x5462;&#xFF1F;</p><blockquote>&#x4F7F;&#x7528;&#x539F;&#x578B;&#x7684;&#x597D;&#x5904;&#x662F;&#x53EF;&#x4EE5;&#x8BA9;&#x6240;&#x6709;&#x5BF9;&#x8C61;&#x5B9E;&#x4F8B;&#x5171;&#x4EAB;&#x5B83;&#x6240;&#x5305;&#x542B;&#x7684;&#x5C5E;&#x6027;&#x548C;&#x65B9;&#x6CD5;&#x3002;</blockquote><p>&#x8F6C;&#x6655;&#x4E86;&#x9EBD;&#xFF1F;&#x662F;&#x4E0D;&#x662F;&#x8D85;&#x7EA7;&#x4E71;&#xFF1F;&#x1F914;&#x53C8;&#x6784;&#x9020;&#x51FD;&#x6570;&#xFF0C;&#x53C8;&#x539F;&#x578B;&#xFF0C;&#x53C8;&#x5B9E;&#x4F8B;&#xFF0C;&#x4E0D;&#x62C5;&#x5FC3;&#xFF0C;&#x6211;&#x4E00;&#x53E5;&#x8BDD;&#x70B9;&#x7834;&#x4F60;<br><strong>&#x6211;&#x4EEC;&#x6240;&#x6709;&#x7684;&#x6784;&#x9020;&#x51FD;&#x6570;&#x6700;&#x7EC8;&#x90FD;&#x8981;&#x6F14;&#x53D8;&#x6210;&#x5B9E;&#x4F8B;&#x624D;&#x6709;&#x610F;&#x4E49;&#xFF0C;&#x56E0;&#x4E3A;&#x5728;&#x6784;&#x9020;&#x51FD;&#x6570;&#x4E2D;&#x5B9A;&#x4E49;&#x65B9;&#x6CD5;&#x65E0;&#x6CD5;&#x88AB;&#x6240;&#x6709;&#x7684;&#x5B9E;&#x4F8B;&#x5171;&#x4EAB;&#xFF0C;&#x56E0;&#x6B64;&#x53EA;&#x80FD;&#x627E;&#x6784;&#x9020;&#x51FD;&#x6570;&#x7684;&#x4E0A;&#x4E00;&#x7EA7;&#xFF0C;&#x5C31;&#x662F;&#x539F;&#x578B;&#xFF0C;&#x5728;&#x539F;&#x578B;&#x4E0A;&#x5B9A;&#x4E49;&#x7684;&#x5C5E;&#x6027;&#x548C;&#x65B9;&#x6CD5;&#x53EF;&#x4EE5;&#x88AB;&#x6240;&#x6709;&#x7684;&#x5B9E;&#x4F8B;&#x6240;&#x5171;&#x4EAB;&#xFF0C;&#x8FD9;&#x5C31;&#x662F;&#x5BF9;&#x539F;&#x578B;&#x5BF9;&#x8C61;&#x7684;&#x6027;&#x8D28;</strong></p><p>&#x770B;&#x4E2A;&#x56FE;&#x4F60;&#x5C31;&#x77E5;&#x9053;&#x4E86;&#xFF0C;&#x5B83;&#x4EEC;&#x4E09;&#x8005;&#x4E4B;&#x95F4;&#x5C31;&#x662F;&#x4E09;&#x89D2;&#x604B;&#x5173;&#x7CFB;&#x1F46A;<br><span class="img-wrap"><img data-src="/img/bVbgjKl?w=800&amp;h=415" src="https://static.alili.tech/img/bVbgjKl?w=800&amp;h=415" alt="&#x56FE;&#x7247;&#x63CF;&#x8FF0;" title="&#x56FE;&#x7247;&#x63CF;&#x8FF0;"></span><br>&#x5F88;&#x901A;&#x4FD7;&#x6613;&#x61C2;&#x4E86;&#x5427;<br>&#x6784;&#x9020;&#x51FD;&#x6570;.prototype = &#x539F;&#x578B;<br>&#x539F;&#x578B;.constructor = &#x6784;&#x9020;&#x51FD;&#x6570;<br>&#x5B9E;&#x4F8B;&#x5BF9;&#x8C61;.constructor = &#x6784;&#x9020;&#x51FD;&#x6570;&#xFF08;&#x8FD9;&#x662F;&#x56E0;&#x4E3A;&#x5B9E;&#x4F8B;&#x5BF9;&#x8C61;&#x5728;&#x81EA;&#x8EAB;&#x627E;&#x4E0D;&#x5230;constructor&#x5C5E;&#x6027;&#xFF0C;&#x90A3;&#x4E48;&#x4ED6;&#x4F1A;&#x901A;&#x8FC7;__proto__&#x53BB;&#x539F;&#x578B;&#x4E2D;&#x627E;&#xFF0C;&#x901A;&#x8FC7;&#x539F;&#x578B;&#x642D;&#x6865;&#x6307;&#x5411;&#x4E86;&#x6784;&#x9020;&#x51FD;&#x6570;&#xFF09;<br>&#x5B9E;&#x4F8B;&#x5BF9;&#x8C61;.__proto__ = &#x539F;&#x578B;</p><p>&#x539F;&#x578B;&#x662F;&#x6253;&#x5370;&#x663E;&#x793A;&#x4E0D;&#x51FA;&#x6765;&#x7684;&#xFF0C;&#x53EA;&#x80FD;&#x901A;&#x8FC7; <strong>&#x6784;&#x9020;&#x51FD;&#x6570;.prototype</strong> &#x53BB;&#x8868;&#x793A;</p><p>&#x4E0B;&#x9762;&#x4ECB;&#x7ECD;&#x53E6;&#x5916;&#x4E24;&#x4E2A;&#x83B7;&#x53D6;&#x539F;&#x578B;&#x7684;&#x65B9;&#x6CD5;&#x1F381;</p><blockquote><strong>isPrototypeOf()&#x65B9;&#x6CD5;</strong>&#xFF1A;&#x7528;&#x4E8E;&#x5224;&#x65AD;&#x8FD9;&#x4E2A;&#x5B9E;&#x4F8B;&#x7684;&#x6307;&#x9488;&#x662F;&#x5426;&#x6307;&#x5411;&#x8FD9;&#x4E2A;&#x539F;&#x578B;&#x3002;<br><strong>Object.getPrototypeOf()&#x65B9;&#x6CD5;</strong>&#xFF1A;&#x83B7;&#x53D6;&#x5B9E;&#x4F8B;&#x7684;&#x539F;&#x578B;&#xFF0C;&#x8FD9;&#x4E2A;&#x65B9;&#x6CD5;&#x652F;&#x6301;&#x7684;&#x6D4F;&#x89C8;&#x5668;&#x6709;IE9+&#x3001;Firefox 3.5+&#x3001;Safari 5+&#x3001;Opera 12+&#x548C;Chrome&#xFF0C;&#x56E0;&#x6B64;&#x6BD4;&#x8F83;&#x63A8;&#x8350;&#x901A;&#x8FC7;&#x8FD9;&#x4E2A;&#x65B9;&#x6CD5;&#x83B7;&#x53D6;&#x5BF9;&#x8C61;&#x7684;&#x539F;&#x578B;&#x3002;</blockquote><pre><code>&#x5047;&#x5B9A;&#x6709;&#x4E2A;Person&#x6784;&#x9020;&#x51FD;&#x6570;&#x548C;person&#x5BF9;&#x8C61;
Person.prototype.isPrototypeof(person)  // &#x8FD4;&#x56DE;true&#x8BF4;&#x660E;&#x524D;&#x8005;&#x662F;person1&#x7684;&#x539F;&#x578B;
Object.getPrototypeOf(person) === Person.prototype // &#x83B7;&#x53D6;person&#x7684;&#x539F;&#x578B;</code></pre><blockquote><strong>&#x591A;&#x4E2A;&#x5BF9;&#x8C61;&#x5B9E;&#x4F8B;&#x5171;&#x4EAB;&#x539F;&#x578B;&#x6240;&#x4FDD;&#x5B58;&#x7684;&#x5C5E;&#x6027;&#x548C;&#x65B9;&#x6CD5;&#x7684;&#x57FA;&#x672C;&#x539F;&#x7406;</strong><br>&#x6BCF;&#x5F53;&#x4EE3;&#x7801;&#x8BFB;&#x53D6;&#x67D0;&#x4E2A;&#x5BF9;&#x8C61;&#x7684;&#x67D0;&#x4E2A;&#x5C5E;&#x6027;&#x65F6;&#xFF0C;&#x90FD;&#x4F1A;&#x6267;&#x884C;&#x4E00;&#x6B21;&#x641C;&#x7D22;&#xFF0C;&#x76EE;&#x6807;&#x662F;&#x5177;&#x6709;&#x7ED9;&#x5B9A;&#x540D;&#x5B57;&#x7684;&#x5C5E;&#x6027;&#x3002;&#x9996;&#x5148;&#x4ECE;&#x5BF9;&#x8C61;&#x5B9E;&#x4F8B;&#x672C;&#x8EAB;&#x5F00;&#x59CB;&#x3002;&#x5982;&#x679C;&#x5728;&#x5B9E;&#x4F8B;&#x4E2D;&#x627E;&#x5230;&#x4E86;&#x5177;&#x6709;&#x7ED9;&#x5B9A;&#x540D;&#x5B57;&#x7684;&#x5C5E;&#x6027;&#xFF0C;&#x5219;&#x8FD4;&#x56DE;&#x8BE5;&#x5C5E;&#x6027;&#x7684;&#x503C;&#xFF1B;&#x5982;&#x679C;&#x6CA1;&#x6709;&#x627E;&#x5230;&#xFF0C;&#x5219;&#x7EE7;&#x7EED;&#x641C;&#x7D22;&#x6307;&#x9488;&#x6307;&#x5411;&#x7684;&#x539F;&#x578B;&#x5BF9;&#x8C61;&#xFF0C;&#x5728;&#x539F;&#x578B;&#x5BF9;&#x8C61;&#x4E2D;&#x67E5;&#x627E;&#x5177;&#x6709;&#x7ED9;&#x5B9A;&#x540D;&#x5B57;&#x7684;&#x5C5E;&#x6027;&#x3002;&#x5982;&#x679C;&#x5728;&#x539F;&#x578B;&#x5BF9;&#x8C61;&#x4E2D;&#x627E;&#x5230;&#x4E86;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#xFF0C;&#x5219;&#x8FD4;&#x56DE;&#x8BE5;&#x5C5E;&#x6027;&#x503C;&#x3002;</blockquote><p>&#x6211;&#x4EEC;&#x53EF;&#x4EE5;&#x8BBF;&#x95EE;&#x539F;&#x578B;&#x4E2D;&#x7684;&#x503C;&#xFF0C;&#x4F46;&#x662F;&#x5374;&#x4E0D;&#x80FD;&#x91CD;&#x5199;&#x539F;&#x578B;&#x4E2D;&#x7684;&#x503C;&#xFF0C;&#x5982;&#x679C;&#x6211;&#x4EEC;&#x5728;&#x5B9E;&#x4F8B;&#x4E2D;&#x6DFB;&#x52A0;&#x4E00;&#x4E2A;&#x5C5E;&#x6027;&#xFF0C;&#x800C;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#x540D;&#x548C;&#x539F;&#x578B;&#x4E2D;&#x7684;&#x91CD;&#x540D;&#xFF0C;&#x5219;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#x5C06;&#x4F1A;&#x5C4F;&#x853D;&#xFF08;&#x590D;&#x5199;&#xFF09;&#x539F;&#x578B;&#x4E2D;&#x7684;&#x90A3;&#x4E2A;&#x5C5E;&#x6027;&#x3002;</p><pre><code>function Person() {}

Person.prototype.name = &quot;George&quot;
Person.prototype.sayName = function() {
    console.log(this.name)
}

let person1 = new Person();
let person2 = new Person();
person1.name = &quot;&#x547D;&#x540D;&#x6700;&#x5934;&#x75DB;&quot;;

// &#x5728;&#x8FD9;&#x4E00;&#x73AF;&#x8282;&#xFF0C;person1.name&#x4F1A;&#x4ECE;&#x4ED6;&#x5B9E;&#x4F8B;&#x4E2D;&#x627E;&#xFF0C;&#x82E5;&#x5B9E;&#x4F8B;&#x6CA1;&#x627E;&#x5230;&#xFF0C;&#x5219;&#x7EE7;&#x7EED;&#x641C;&#x7D22;&#x5B83;&#x7684;&#x539F;&#x578B;&#x5BF9;&#x8C61;
console.log(person1.name); // &#x547D;&#x540D;&#x6700;&#x5934;&#x75DB; 
console.log(person2.name); // George</code></pre><p>&#x5728;&#x5B9E;&#x4F8B;&#x5BF9;&#x8C61;&#x4E2D;&#x6DFB;&#x52A0;&#x4E00;&#x5C5E;&#x6027;&#x53EA;&#x4F1A;&#x963B;&#x6B62;&#x6211;&#x4EEC;&#x8BBF;&#x95EE;&#x539F;&#x578B;&#x4E2D;&#x7684;&#x90A3;&#x4E2A;&#x5C5E;&#x6027;&#xFF0C;&#x4F46;&#x4E0D;&#x4F1A;&#x4FEE;&#x6539;&#x90A3;&#x4E2A;&#x5C5E;&#x6027;&#x3002;<strong>&#x5373;&#x4F7F;&#x5C06;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#x8BBE;&#x7F6E;&#x4E3A;null&#xFF0C;&#x4E5F;&#x53EA;&#x4F1A;&#x5728;&#x5B9E;&#x4F8B;&#x4E2D;&#x8BBE;&#x7F6E;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#xFF0C;&#x800C;&#x4E0D;&#x4F1A;&#x6062;&#x590D;&#x5176;&#x6307;&#x5411;&#x539F;&#x578B;&#x7684;&#x8FDE;&#x63A5;</strong>&#x3002;</p><p>&#x82E5;&#x60F3;&#x5B8C;&#x5168;&#x5220;&#x9664;&#x5B9E;&#x4F8B;&#x5C5E;&#x6027;&#xFF0C;&#x53EF;&#x4F7F;&#x7528;delete&#x64CD;&#x4F5C;&#x7B26;&#xFF0C;&#x4ECE;&#x800C;&#x8BA9;&#x6211;&#x4EEC;&#x80FD;&#x591F;&#x91CD;&#x65B0;&#x8BBF;&#x95EE;&#x539F;&#x578B;&#x4E2D;&#x7684;&#x5C5E;&#x6027;&#x3002;</p><h3>delete &#x64CD;&#x4F5C;&#x7B26;&#x7684;&#x4F7F;&#x7528;</h3><pre><code>&#x4F9D;&#x65E7;&#x7528;&#x4E0A;&#x9762;&#x90A3;&#x4E2A;&#x4F8B;&#x5B50;
delete&#x64CD;&#x4F5C;&#x7B26;&#x53EF;&#x7528;&#x4E8E;&#x5220;&#x9664;&#x5BF9;&#x8C61;&#x7684;&#x5C5E;&#x6027;&#xFF0C;&#x65E0;&#x8BBA;&#x662F;&#x5B9E;&#x4F8B;&#x4E0A;&#x7684;&#x5C5E;&#x6027;&#xFF0C;&#x8FD8;&#x662F;&#x5728;&#x539F;&#x578B;&#x4E0A;&#x7684;&#x5C5E;&#x6027;&#x90FD;&#x53EF;&#x4EE5;&#x5220;

delete person1.name    // &#x5220;&#x9664;&#x8FD9;&#x4E2A;&#x5B9E;&#x4F8B;&#x7684;&#x5C5E;&#x6027;
delete Person.prototype.name    // &#x5220;&#x9664;&#x539F;&#x578B;&#x4E0A;&#x7684;&#x5C5E;&#x6027;
delete Person.prototype.constructor // &#x5220;&#x9664;constructor&#x5C5E;&#x6027;&#xFF0C;&#x8FD9;&#x6837;&#x5C31;&#x6CA1;&#x529E;&#x6CD5;&#x6307;&#x56DE;&#x51FD;&#x6570;&#x4E86;</code></pre><blockquote>hasOwnProperty()&#x65B9;&#x6CD5;&#x53EF;&#x7528;&#x6765;&#x68C0;&#x6D4B;&#x4E00;&#x4E2A;&#x5C5E;&#x6027;&#x662F;&#x5B58;&#x5728;&#x4E8E;&#x5B9E;&#x4F8B;&#x4E2D;&#xFF0C;&#x8FD8;&#x662F;&#x5B58;&#x5728;&#x4E8E;&#x539F;&#x578B;&#x4E2D;&#x3002;&#x8FD9;&#x4E2A;&#x65B9;&#x6CD5;&#x53EA;&#x5728;&#x7ED9;&#x5B9A;&#x5C5E;&#x6027;&#x5B58;&#x5728;&#x4E8E;&#x5BF9;&#x8C61;&#x5B9E;&#x4F8B;&#x65F6;&#xFF0C;&#x624D;&#x8FD4;&#x56DE;true&#xFF0C;&#x4E5F;&#x53EF;&#x4EE5;&#x8FD9;&#x6837;&#x7406;&#x89E3;&#xFF0C;hasOwnProperty&#x65B9;&#x6CD5;&#x7528;&#x4E8E;&#x68C0;&#x6D4B;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#x662F;&#x5426;&#x662F;&#x5BF9;&#x8C61;&#x672C;&#x8EAB;&#x5C5E;&#x6027;&#x3002;<br>obj.hasOwnProperty(&apos;&#x5C5E;&#x6027;&#x540D;&apos;)</blockquote><p>Demo&#xFF1A;</p><pre><code>function Person(){ 
  this.name = &apos;&#x547D;&#x540D;&#x6700;&#x5934;&#x75DB;&apos;
}
var person = new Person()
Person.prototype.age = &apos;18&apos;
console.log(person.hasOwnProperty(&apos;name&apos;))  // true
console.log(Person.prototype.hasOwnProperty(&apos;age&apos;)) // true</code></pre><h3>in&#x64CD;&#x4F5C;&#x7B26;</h3><blockquote>in&#x64CD;&#x4F5C;&#x7B26;&#x6709;&#x4E24;&#x79CD;&#x7528;&#x6CD5;<br>&#x2460;&#x653E;&#x5728;for-in&#x5FAA;&#x73AF;&#x4E2D;&#x4F7F;&#x7528;&#xFF0C;for-in&#x80FD;&#x591F;&#x8FD4;&#x56DE;&#x6240;&#x6709;&#x80FD;&#x591F;&#x901A;&#x8FC7;&#x5BF9;&#x8C61;&#x8BBF;&#x95EE;&#x7684;&#x3001;&#x53EF;&#x679A;&#x4E3E;&#x7684;(enumerable)&#x5C5E;&#x6027;&#xFF08;&#x53EF;&#x679A;&#x4E3E;&#x5C5E;&#x6027;&#x53EF;&#x53C2;&#x770B;<a href="https://segmentfault.com/a/1190000015890022">&#x4E00;&#x773C;&#x770B;&#x7A7F;&#x1F440;JS&#x5BF9;&#x8C61;</a>&#x4E2D;&#x5BF9;&#x8C61;&#x5C5E;&#x6027;&#x90E8;&#x5206;&#xFF09;&#x5176;&#x4E2D;&#xFF0C;&#x65E2;&#x5305;&#x62EC;&#x5B58;&#x5728;&#x4E8E;&#x5B9E;&#x4F8B;&#x4E2D;&#x7684;&#x5C5E;&#x6027;&#xFF0C;&#x4E5F;&#x5305;&#x62EC;&#x5B58;&#x5728;&#x4E8E;&#x539F;&#x578B;&#x4E2D;&#x7684;&#x5C5E;&#x6027;&#xFF0C;&#x5C4F;&#x853D;&#x4E86;&#x6240;&#x6709;&#x4E0D;&#x53EF;&#x679A;&#x4E3E;&#x7684;&#x5C5E;&#x6027;<br>&#x2461;&#x5355;&#x72EC;&#x4F7F;&#x7528;&#x65F6;&#xFF0C;in&#x64CD;&#x4F5C;&#x7B26;&#x4F1A;&#x5728;&#x901A;&#x8FC7;&#x5BF9;&#x8C61;&#x80FD;&#x591F;&#x8BBF;&#x95EE;&#x7ED9;&#x5B9A;&#x5C5E;&#x6027;&#x65F6;&#x8FD4;&#x56DE;true&#xFF0C;&#x65E0;&#x8BBA;&#x8BE5;&#x5C5E;&#x6027;&#x5B58;&#x5728;&#x4E8E;&#x5B9E;&#x4F8B;&#x4E2D;&#x8FD8;&#x662F;&#x539F;&#x578B;&#x4E2D;&#x3002;&#x8BF4;&#x767D;&#x4E86;&#x5C31;&#x662F;&#xFF0C;&#x53EF;&#x4EE5;&#x901A;&#x8FC7;in&#x64CD;&#x4F5C;&#x7B26;&#x5224;&#x65AD;&#x8FD9;&#x4E2A;&#x5BF9;&#x8C61;&#x662F;&#x5426;&#x6709;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#x3002;in&#x64CD;&#x4F5C;&#x7B26;&#x4F1A;&#x5148;&#x5728;&#x5B9E;&#x4F8B;&#x4E2D;&#x5BFB;&#x627E;&#x5C5E;&#x6027;&#xFF0C;&#x5BFB;&#x627E;&#x65E0;&#x679C;&#x518D;&#x53BB;&#x539F;&#x578B;&#x4E2D;&#x5BFB;&#x627E;&#xFF0C;&#x4F46;&#x4E0D;&#x53EF;&#x4EE5;&#x9006;&#x5411;&#x67E5;&#x627E;&#x3002;</blockquote><p>&#x4E3E;&#x4E2A;&#x1F330;&#xFF08;in &#x5355;&#x72EC;&#x4F7F;&#x7528;&#xFF09;</p><pre><code>function Person(){}
var person = new Person()
// name&#x5B58;&#x5728;&#x4E8E;&#x5B9E;&#x4F8B;&#x4E2D;
person.name = &apos;&#x547D;&#x540D;&#x6700;&#x5934;&#x75DB;&apos;
// age&#x5B58;&#x5728;&#x4E8E;&#x539F;&#x578B;&#x4E2D;
Person.prototype.age = &apos;18&apos;
console.log(&apos;name&apos; in person)  // true
console.log(&apos;name&apos; in Person.prototype) // false &#x4E0D;&#x53EF;&#x9006;&#x5411;&#x67E5;&#x627E;&#xFF0C;&#x539F;&#x578B;&#x4E2D;&#x4E0D;&#x80FD;&#x627E;&#x5230;&#x5B9E;&#x4F8B;&#x4E2D;&#x5C5E;&#x6027;
console.log(&apos;age&apos; in person)  // true
console.log(&apos;age&apos; in Person.prototype) // true</code></pre><p>&#x6211;&#x4EEC;&#x53EF;&#x4EE5;&#x6784;&#x9020;&#x4E00;&#x4E2A;&#x51FD;&#x6570;&#xFF0C;&#x7528;&#x4E8E;&#x5224;&#x65AD;&#x4E00;&#x4E2A;&#x5C5E;&#x6027;&#x662F;&#x5728;&#x539F;&#x578B;&#x4E2D;&#x8FD8;&#x662F;&#x5728;&#x5BF9;&#x8C61;&#x5B9E;&#x4F8B;&#x4E2D;&#xFF0C;&#x540C;&#x65F6;&#x4F7F;&#x7528;in&#x548C;hasOwnProperty()&#x65B9;&#x6CD5;&#x53EF;&#x4EE5;&#x5B9E;&#x73B0;&#x8FD9;&#x4E2A;&#x51FD;&#x6570;&#x7684;&#x6784;&#x9020;</p><pre><code>// &#x5224;&#x65AD;&#x4E00;&#x4E2A;&#x5C5E;&#x6027;&#x662F;&#x5426;&#x5728;&#x539F;&#x578B;&#x4E2D;
function hasPrototypeProperty(object&#xFF0C;name) {
    return (name in object) &amp;&amp; !object.hasOwnProperty(name)
}</code></pre><h3>for-in&#x3001;Object.keys()&#x548C;Object.getOwnPropertyNames()</h3><blockquote>for-in&#x548C;Object.keys&#x90FD;&#x662F;&#x7528;&#x4E8E;&#x904D;&#x5386;<strong>&#x53EF;&#x679A;&#x4E3E;</strong>&#x5BF9;&#x8C61;&#x5C5E;&#x6027;&#x7684;&#xFF0C;&#x4ED6;&#x4EEC;&#x7684;&#x4E3B;&#x8981;&#x533A;&#x522B;&#x5728;&#x4E8E;<br>for-in&#xFF1A;<strong>&#x904D;&#x5386;&#x5BF9;&#x8C61;&#x4E0A;&#x6240;&#x6709;&#x53EF;&#x679A;&#x4E3E;&#x7684;&#x5C5E;&#x6027;&#xFF0C;&#x5305;&#x62EC;&#x539F;&#x578B;&#x4E0A;&#x7684;&#xFF08;&#x4F1A;&#x5728;&#x539F;&#x578B;&#x4E0A;&#x5BFB;&#x627E;&#xFF09;</strong><br>Object.keys()&#xFF1A;<strong>&#x53EA;&#x904D;&#x5386;&#x81EA;&#x8EAB;&#x7684;&#x53EF;&#x679A;&#x4E3E;&#x5C5E;&#x6027;&#xFF0C;&#x8FD4;&#x56DE;&#x4E00;&#x4E2A;&#x5C5E;&#x6027;&#x6570;&#x7EC4;&#xFF08;&#x4E0D;&#x4F1A;&#x5728;&#x539F;&#x578B;&#x4E0A;&#x5BFB;&#x627E;&#xFF09;</strong><p>Object.getOwnPropertyNames&#xFF1A;<strong>&#x83B7;&#x53D6;&#x81EA;&#x8EAB;&#x6240;&#x6709;&#x5C5E;&#x6027;&#xFF0C;&#x65E0;&#x8BBA;&#x5B83;&#x662F;&#x5426;&#x53EF;&#x679A;&#x4E3E;</strong></p></blockquote><pre><code>function Person() {}
let person = new Person()
// &#x5B9E;&#x4F8B;&#x4E0A;&#x5B9A;&#x4E49;&#x5C5E;&#x6027;
Object.defineProperties(person, {
  name: {
    value: &apos;&#x547D;&#x540D;&#x6700;&#x5934;&#x75DB;&apos;,
    enumerable: true
  },
  age: {
    value: 18
  }
}) 
// &#x539F;&#x578B;&#x4E0A;&#x5B9A;&#x4E49;&#x5C5E;&#x6027;
Object.defineProperties(Object.getPrototypeOf(person), {
  year: {
    value: 2018,
    enumerable: true
  },
  job: {
    value: &apos;programer&apos;
  },
  demo: {
    enumerable: true,
    get() {
      return this.year
    }
  }
})
for(let i in person) {
  console.log(i, person[i]) 
  // name &#x547D;&#x540D;&#x6700;&#x5934;&#x75DB;
  // year 2018
  // demo 2018
}
for(let i in Object.getPrototypeOf(person)){
  console.log(i, Object.getPrototypeOf(person)[i])
  // year 2018
  // demo 2018
}
console.log(Object.keys(person)) // [&apos;name&apos;]
console.log(Object.getOwnPropertyNames(person)) // [&quot;name&quot;, &quot;age&quot;]
console.log(Object.getOwnPropertyNames(Person)) // [&quot;length&quot;, &quot;name&quot;, &quot;prototype&quot;]
console.log(Object.getOwnPropertyNames(Person.prototype)) // [&quot;constructor&quot;, &quot;year&quot;, &quot;job&quot;, &quot;demo&quot;]</code></pre><h3>&#x4F7F;&#x7528;&#x5B57;&#x9762;&#x91CF;&#x65B9;&#x5F0F;&#x521B;&#x5EFA;&#x51FD;&#x6570;&#x539F;&#x578B;</h3><p>&#x4E0A;&#x9762;&#x6211;&#x4EEC;&#x4ECB;&#x7ECD;&#x4E86;&#x901A;&#x8FC7;&#x6784;&#x9020;&#x51FD;&#x6570;&#x65B9;&#x5F0F;&#x521B;&#x5EFA;&#x51FD;&#x6570;&#x539F;&#x578B;&#xFF0C;&#x4E0B;&#x9762;&#x4ECB;&#x7ECD;&#x4E00;&#x79CD;&#x901A;&#x8FC7;&#x5B57;&#x9762;&#x91CF;&#x7684;&#x65B9;&#x5F0F;&#x521B;&#x5EFA;&#x51FD;&#x6570;&#x539F;&#x578B;&#x7684;&#x65B9;&#x6CD5;</p><pre><code>function Person() {}
Person.prototype = {
    name: &apos;&#x547D;&#x540D;&#x6700;&#x5934;&#x75DB;&apos;&#xFF0C;
    age: 18,
    sayName: function(){
        console.log(this.name)
    }
}</code></pre><p>&#x867D;&#x7136;&#x8FD9;&#x79CD;&#x521B;&#x5EFA;&#x65B9;&#x5F0F;&#x76F8;&#x5BF9;&#x4E8E;&#x6784;&#x9020;&#x51FD;&#x6570;&#x65B9;&#x5F0F;&#x5728;&#x89C6;&#x89C9;&#x4E0A;&#x6709;&#x66F4;&#x597D;&#x7684;&#x5C01;&#x88C5;&#x6027;&#xFF0C;&#x4F46;&#x662F;&#x8FD9;&#x79CD;&#x65B9;&#x5F0F;&#x521B;&#x5EFA;&#x5BF9;&#x8C61;&#x6709;&#x4E2A;&#x4F8B;&#x5916;&#xFF0C;&#x90A3;&#x5C31;&#x662F;constructor&#x5C5E;&#x6027;&#x4E0D;&#x518D;&#x6307;&#x5411;Person&#x4E86;&#xFF0C;&#x56E0;&#x4E3A;<strong>&#x6BCF;&#x521B;&#x5EFA;&#x4E00;&#x4E2A;&#x51FD;&#x6570;&#xFF0C;&#x5C31;&#x4F1A;&#x540C;&#x65F6;&#x521B;&#x5EFA;&#x5B83;&#x7684;prototype&#x5BF9;&#x8C61;&#xFF0C;&#x8FD9;&#x4E2A;&#x5BF9;&#x8C61;&#x4F1A;&#x81EA;&#x52A8;&#x83B7;&#x5F97;constructor&#x5C5E;&#x6027;</strong>&#x3002;&#x800C;&#x5B57;&#x9762;&#x91CF;&#x8FD9;&#x79CD;&#x5199;&#x6CD5;&#xFF0C;&#x4F1A;&#x91CD;&#x5199;&#x9ED8;&#x8BA4;&#x7684;prototype&#x5BF9;&#x8C61;&#xFF0C;&#x56E0;&#x6B64;constructor&#x5C5E;&#x6027;&#x4E5F;&#x5C31;&#x53D8;&#x6210;&#x4E86;&#x65B0;&#x5BF9;&#x8C61;&#x7684;constructor&#x5C5E;&#x6027;&#xFF08;&#x6307;&#x5411;Object&#x6784;&#x9020;&#x51FD;&#x6570;&#xFF09;&#x4E0D;&#x518D;&#x6307;&#x5411;Person&#x51FD;&#x6570;&#x4E86;&#xFF0C;&#x6B64;&#x65F6;&#xFF0C;&#x5C3D;&#x7BA1;instanceof&#x64CD;&#x4F5C;&#x7B26;&#x8FD8;&#x80FD;&#x8FD4;&#x56DE;&#x6B63;&#x786E;&#x7684;&#x7ED3;&#x679C;&#xFF0C;&#x4F46;&#x901A;&#x8FC7;constructor&#x5374;&#x65E0;&#x6CD5;&#x786E;&#x5B9A;&#x5BF9;&#x8C61;&#x7684;&#x7C7B;&#x578B;&#x3002;</p><pre><code>function Person() {}
let person = new Person()
console.log(person instanceof Object) // true
console.log(person instanceof Person) // true
console.log(person.constructor === Person) // false
console.log(person.constructor === Object) // true</code></pre><p>&#x82E5;&#x60F3;&#x8BA9;&#x5B57;&#x9762;&#x91CF;&#x65B9;&#x5F0F;&#x521B;&#x5EFA;&#x539F;&#x578B;&#x7684;constructor&#x91CD;&#x65B0;&#x6307;&#x5411;Person&#xFF0C;&#x53EA;&#x7528;&#x523B;&#x610F;&#x4E3A;&#x5B83;&#x8BBE;&#x7F6E;&#x503C;&#x5373;&#x53EF;</p><pre><code>function Person() {}
Person.prototype = {
    constructor: Person,
    name: &apos;&#x547D;&#x540D;&#x6700;&#x5934;&#x75DB;&apos;
    ...
}</code></pre><p>&#x8FD9;&#x6837;&#x8BBE;&#x7F6E;&#x8FD8;&#x662F;&#x6709;&#x4E2A;&#x9690;&#x60A3;&#x7684;&#xFF0C;&#x56E0;&#x4E3A;&#x6211;&#x4EEC;&#x77E5;&#x9053;&#xFF0C;&#x76F4;&#x63A5;&#x5B9A;&#x4E49;&#x5C5E;&#x6027;&#x7684;&#x65B9;&#x5F0F;&#x4F1A;&#x5BFC;&#x81F4;&#x5C5E;&#x6027;&#x7279;&#x6027;&#x9ED8;&#x8BA4;&#x503C;&#x4E3A;true&#xFF0C;&#x8FD9;&#x6837;&#x5B9A;&#x4E49;&#x7684;constructor[[Enumerable]]&#x7279;&#x6027;&#x88AB;&#x8BBE;&#x7F6E;&#x4E3A;true&#xFF0C;&#x800C;&#x539F;&#x751F;&#x7684;constructor&#x662F;&#x4E0D;&#x53EF;&#x679A;&#x4E3E;&#x7684;&#xFF0C;&#x56E0;&#x65E2;&#x60F3;&#x5B9E;&#x73B0;constructor&#x6307;&#x5411;&#xFF0C;&#x53C8;&#x60F3;&#x8BA9;[[Enumerable]]&#x7279;&#x6027;&#x88AB;&#x8BBE;&#x7F6E;&#x4E3A;true&#xFF0C;&#x53EA;&#x80FD;&#x901A;&#x8FC7;Object.defineProperty()&#x65B9;&#x6CD5;&#x6765;&#x5199;constructor</p><pre><code>function Person() {}
Person.prototype = {
    name: &apos;&#x547D;&#x540D;&#x6700;&#x5934;&#x75DB;&apos;,
    ...
}
Object.defineProperty(Person.prototype, &apos;constructor&apos;, {
    enumerable: false,
    value: Person
})</code></pre><h3>&#x539F;&#x578B;&#x7684;&#x52A8;&#x6001;&#x6027;</h3><p>&#x7528;&#x4E00;&#x53E5;&#x8BDD;&#x8BF4;&#x660E;&#x767D;&#x5C31;&#x662F;<strong>&#x539F;&#x578B;&#x7684;&#x53D8;&#x5316;&#x53EF;&#x4EE5;&#x901A;&#x8FC7;&#x5B9E;&#x4F8B;&#x53CD;&#x5E94;&#x51FA;&#x6765;&#xFF0C;&#x53EF;&#x4EE5;&#x5148;&#x521B;&#x5EFA;&#x5B9E;&#x4F8B;&#xFF0C;&#x518D;&#x5B9A;&#x4E49;&#x6216;&#x4FEE;&#x6539;&#x539F;&#x578B;&#x4E0A;&#x7684;&#x5C5E;&#x6027;&#x3002;</strong>&#x56E0;&#x4E3A;<strong>&#x5B9E;&#x4F8B;&#x4E0E;&#x539F;&#x578B;&#x4E4B;&#x95F4;&#x7684;&#x8FDE;&#x63A5;&#x662F;&#x4E00;&#x4E2A;&#x6307;&#x9488;&#xFF0C;&#x800C;&#x975E;&#x4E00;&#x4E2A;&#x526F;&#x672C;&#xFF0C;&#x56E0;&#x6B64;&#x53EF;&#x4EE5;&#x5728;&#x539F;&#x578B;&#x4E2D;&#x627E;&#x5230;&#x65B0;&#x7684;&#x5C5E;&#x6027;&#x5E76;&#x8FD4;&#x56DE;&#x4FDD;&#x5B58;&#x90A3;&#x91CC;&#x7684;&#x51FD;&#x6570;&#x3002;</strong>&#x8FD9;&#x79CD;&#x52A8;&#x6001;&#x6027;&#x4F1A;&#x5728;&#x591A;&#x4E2A;&#x5B9E;&#x4F8B;&#x4E2D;&#x76F8;&#x4E92;&#x5F71;&#x54CD;&#xFF0C;&#x5373;&#x5176;&#x4E2D;&#x4E00;&#x4E2A;&#x5B9E;&#x4F8B;&#x4FEE;&#x6539;&#x4E86;&#x539F;&#x578B;&#x4E0A;&#x7684;&#x5185;&#x5BB9;&#xFF0C;&#x4E5F;&#x80FD;&#x7ACB;&#x523B;&#x5728;&#x6240;&#x6709;&#x5B9E;&#x4F8B;&#x4E2D;&#x53CD;&#x6620;&#x51FA;&#x6765;&#x3002;&#x8FD9;&#x4E2A;&#x539F;&#x56E0;&#x5F52;&#x7ED3;&#x4E3A;<strong>&#x5B9E;&#x4F8B;&#x4E0E;&#x539F;&#x578B;&#x4E4B;&#x95F4;&#x7684;&#x677E;&#x6563;&#x94FE;&#x63A5;&#x5173;&#x7CFB;</strong>&#x3002;</p><p>&#x5C3D;&#x7BA1;&#x53EF;&#x4EE5;&#x968F;&#x65F6;&#x5728;&#x539F;&#x578B;&#x4E2D;&#x6DFB;&#x52A0;&#x5C5E;&#x6027;&#x548C;&#x65B9;&#x6CD5;&#xFF0C;&#x5E76;&#x4E14;&#x4FEE;&#x6539;&#x7684;&#x503C;&#x80FD;&#x591F;&#x7ACB;&#x523B;&#x5728;&#x6240;&#x6709;&#x5BF9;&#x8C61;&#x5B9E;&#x4F8B;&#x4E2D;&#x53CD;&#x6620;&#x51FA;&#x6765;&#xFF0C;&#x4F46;&#x662F;&#x5982;&#x679C;&#x91CD;&#x65B0;&#x6574;&#x4E2A;&#x539F;&#x578B;&#x5BF9;&#x8C61;&#xFF0C;&#x7ED3;&#x679C;&#x5C31;&#x4E0D;&#x4E00;&#x6837;&#x4E86;&#x3002;<strong>&#x5728;&#x8C03;&#x7528;&#x6784;&#x9020;&#x51FD;&#x6570;&#x65F6;&#x4F1A;&#x4E3A;&#x5B9E;&#x4F8B;&#x6DFB;&#x52A0;&#x4E00;&#x4E2A;&#x6307;&#x5411;&#x6700;&#x521D;&#x6307;&#x5411;&#x539F;&#x578B;&#x7684;[[prototype]]&#x6307;&#x9488;&#xFF0C;&#x628A;&#x539F;&#x578B;&#x4FEE;&#x6539;&#x4E3A;&#x53E6;&#x4E00;&#x4E2A;&#x5BF9;&#x8C61;&#x5C31;&#x7B49;&#x4E8E;&#x5207;&#x65AD;&#x4E86;&#x6784;&#x9020;&#x51FD;&#x6570;&#x4E0E;&#x6700;&#x521D;&#x539F;&#x578B;&#x4E4B;&#x95F4;&#x7684;&#x8054;&#x7CFB;</strong>&#xFF0C;&#x8BB0;&#x4F4F;&#xFF1A;<strong>&#x5B9E;&#x4F8B;&#x4E2D;&#x7684;&#x6307;&#x9488;&#x4EC5;&#x6307;&#x5411;&#x539F;&#x578B;&#xFF0C;&#x800C;&#x4E0D;&#x6307;&#x5411;&#x6784;&#x9020;&#x51FD;&#x6570;</strong></p><pre><code>function Person() {}
let person = new Person();
Person.prototype = {
  constructor: Person,
  name: &apos;&#x547D;&#x540D;&#x6700;&#x5934;&#x75DB;&apos;,
  sayName: function(){
    console.log(this.name) // &#x56E0;&#x4E3A;&#x91CD;&#x5199;&#x5B8C;&#x540E;this&#x7684;&#x6307;&#x5411;&#x5C31;&#x53D8;&#x4E86;
  }
}
person.sayName() // error
console.log(person.name) //undefined</code></pre><p><span class="img-wrap"><img data-src="/img/bVbfzoD?w=1476&amp;h=1238" src="https://static.alili.tech/img/bVbfzoD?w=1476&amp;h=1238" alt="&#x56FE;&#x7247;&#x63CF;&#x8FF0;" title="&#x56FE;&#x7247;&#x63CF;&#x8FF0;"></span></p><p>&#x4E5F;&#x5C31;&#x662F;&#x8BF4;&#xFF0C;&#x4F60;&#x53EF;&#x4EE5;&#x5728;&#x539F;&#x578B;&#x4E0A;&#x5B9A;&#x4E49;&#x65B0;&#x5C5E;&#x6027;&#xFF0C;&#x4F46;&#x662F;&#x5C3D;&#x91CF;&#x4E0D;&#x8981;&#x91CD;&#x5199;&#x539F;&#x578B;&#x5BF9;&#x8C61;&#xFF0C;&#x56E0;&#x4E3A;&#x8FD9;&#x4F1A;&#x5BFC;&#x81F4;&#x4E4B;&#x524D;&#x5B9E;&#x4F8B;&#x65E0;&#x6CD5;&#x6307;&#x65B0;&#x5B9A;&#x4E49;&#x7684;&#x539F;&#x578B;&#x3002;<br>&#x4E0B;&#x9762;&#x901A;&#x8FC7;&#x4EE3;&#x7801;&#x8BF4;&#x660E;&#x8FD9;&#x4E00;&#x73B0;&#x8C61;</p><pre><code>function Person() {}
let person = new Person();
Person.prototype.oldName=&apos;George&apos;
console.log(person.oldName) // George

Person.prototype = {
  constructor: Person,
  name: &apos;&#x547D;&#x540D;&#x6700;&#x5934;&#x75DB;&apos;,
  sayName: function(){
    console.log(this.name)
  }
}
// &#x91CD;&#x5199;&#x539F;&#x578B;&#x5BF9;&#x8C61;&#x540E;&#xFF0C;&#x4E0E;&#x5B9E;&#x4F8B;&#x4E4B;&#x95F4;&#x7684;&#x8054;&#x7CFB;&#x88AB;&#x5207;&#x65AD;&#x4E86;
console.log(person.name) // undefined
 
// &#x53EA;&#x80FD;&#x751F;&#x6210;&#x65B0;&#x5B9E;&#x4F8B;&#x624D;&#x80FD;&#x8BBF;&#x95EE;&#x65B0;&#x5B9A;&#x4E49;&#x7684;&#x539F;&#x578B;
let person1 = new Person();
console.log(person1.name) // &#x547D;&#x540D;&#x6700;&#x5934;&#x75DB;</code></pre><h3>&#x539F;&#x751F;&#x5BF9;&#x8C61;&#x7684;&#x539F;&#x578B;</h3><blockquote>&#x539F;&#x578B;&#x6A21;&#x5F0F;&#x7684;&#x91CD;&#x8981;&#x6027;&#x4E0D;&#x4EC5;&#x4F53;&#x73B0;&#x5728;&#x521B;&#x5EFA;&#x81EA;&#x5B9A;&#x4E49;&#x7C7B;&#x578B;&#x65B9;&#x9762;&#xFF0C;&#x5C31;&#x8FDE;&#x6240;&#x6709;&#x539F;&#x751F;&#x7684;&#x5F15;&#x7528;&#x7C7B;&#x578B;&#xFF0C;&#x90FD;&#x662F;&#x91C7;&#x7528;&#x8FD9;&#x79CD;&#x6A21;&#x5F0F;&#x521B;&#x5EFA;&#x7684;&#x3002;&#x6240;&#x6709;&#x539F;&#x751F;&#x5F15;&#x7528;&#x7C7B;&#x578B;&#xFF08;Object&#x3001;Array&#x3001;String&#x7B49;&#x7B49;&#xFF09;&#x90FD;&#x5728;&#x5176;&#x6784;&#x9020;&#x51FD;&#x6570;&#x7684;&#x539F;&#x578B;&#x4E0A;&#x5B9A;&#x4E49;&#x4E86;&#x65B9;&#x6CD5;&#x3002;&#x901A;&#x8FC7;&#x539F;&#x751F;&#x5BF9;&#x8C61;&#x7684;&#x539F;&#x578B;&#xFF0C;&#x4E0D;&#x4EC5;&#x53EF;&#x4EE5;&#x53D6;&#x5F97;&#x6240;&#x6709;&#x9ED8;&#x8BA4;&#x65B9;&#x6CD5;&#x7684;&#x5F15;&#x7528;&#xFF0C;&#x800C;&#x4E14;&#x4E5F;&#x53EF;&#x4EE5;&#x5B9A;&#x4E49;&#x65B0;&#x65B9;&#x6CD5;&#x3002;</blockquote><p>&#x1F330;<br>&#x4E3A;&#x539F;&#x751F;&#x5BF9;&#x8C61;String&#x6DFB;&#x52A0;&#x65B0;&#x65B9;&#x6CD5;newWay</p><pre><code>String.prototype.newWay = function(val) {
   return val
}</code></pre><h3>&#x539F;&#x578B;&#x5BF9;&#x8C61;&#x7684;&#x95EE;&#x9898;</h3><p>&#x539F;&#x578B;&#x5BF9;&#x8C61;&#x7701;&#x7565;&#x4E86;&#x4E3A;&#x6784;&#x9020;&#x51FD;&#x6570;&#x4F20;&#x9012;&#x521D;&#x59CB;&#x5316;&#x53C2;&#x6570;&#x8FD9;&#x4E00;&#x73AF;&#x8282;&#xFF0C;&#x7ED3;&#x679C;&#x6240;&#x6709;&#x5B9E;&#x4F8B;&#x5728;&#x9ED8;&#x8BA4;&#x60C5;&#x51B5;&#x4E0B;&#x90FD;&#x5C06;&#x53D6;&#x5F97;&#x76F8;&#x540C;&#x7684;&#x5C5E;&#x6027;&#x503C;&#xFF0C;&#x867D;&#x7136;&#x8FD9;&#x4F1A;&#x5728;&#x67D0;&#x4E9B;&#x60C5;&#x51B5;&#x4E0B;&#x4F1A;&#x6709;&#x4E9B;&#x4E0D;&#x65B9;&#x4FBF;&#xFF0C;&#x4F46;&#x8FD8;&#x4E0D;&#x662F;&#x539F;&#x578B;&#x7684;&#x6700;&#x5927;&#x95EE;&#x9898;&#xFF0C;&#x539F;&#x578B;&#x6A21;&#x5F0F;&#x7684;&#x6700;&#x5927;&#x95EE;&#x9898;&#x662F;<strong>&#x7531;&#x5176;&#x5171;&#x4EAB;&#x672C;&#x6027;&#x6240;&#x5BFC;&#x81F4;&#x7684;</strong>&#x3002;&#x5373;&#x539F;&#x578B;&#x7684;&#x52A8;&#x6001;&#x6027;&#xFF0C;&#x5176;&#x4E2D;&#x4E00;&#x4E2A;&#x5B9E;&#x4F8B;&#x4FEE;&#x6539;&#x4E86;&#x539F;&#x578B;&#x4E0A;&#x7684;&#x5185;&#x5BB9;&#xFF0C;&#x4E5F;&#x80FD;&#x7ACB;&#x523B;&#x5728;&#x6240;&#x6709;&#x5B9E;&#x4F8B;&#x4E2D;&#x53CD;&#x6620;&#x51FA;&#x6765;&#x3002;</p><p>&#x5171;&#x4EAB;&#x672C;&#x6027;&#x5C31;&#x662F;&#x53CC;&#x5203;&#x5251;<br>&#x5982;&#x679C;&#x6211;&#x4EEC;&#x671F;&#x671B;&#xFF0C;&#x6240;&#x6709;&#x5B9E;&#x4F8B;&#x5171;&#x4EAB;&#x4E00;&#x4E2A;&#x5C5E;&#x6027;&#x503C;&#xFF0C;&#x90A3;&#x539F;&#x578B;&#x65B9;&#x6CD5;&#x53EF;&#x4EE5;&#x5F88;&#x597D;&#x89E3;&#x51B3;&#x8FD9;&#x4E2A;&#x95EE;&#x9898;&#xFF0C;&#x4F46;&#x662F;&#x5982;&#x679C;&#x6211;&#x4EEC;&#x671F;&#x671B;&#x6BCF;&#x4E2A;&#x5B9E;&#x4F8B;&#x90FD;&#x6709;&#x5C5E;&#x4E8E;&#x81EA;&#x5DF1;&#x7684;&#x5C5E;&#x6027;&#xFF0C;&#x628A;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#x503C;&#x5B9A;&#x4E49;&#x5728;&#x539F;&#x578B;&#x4E0A;&#x5C31;&#x4F1A;&#x76F8;&#x4E92;&#x6709;&#x5F71;&#x54CD;&#x4E86;&#x3002;</p><h1>&#x5C0F;&#x7ED3;</h1><ul><li>&#x6784;&#x9020;&#x51FD;&#x6570;&#x521B;&#x5EFA;&#x51FA;&#x6765;&#xFF0C;&#x4F1A;&#x6709;&#x4E00;&#x4E2A;&#x539F;&#x578B;&#x5C5E;&#x6027;prototype&#xFF0C;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#x662F;&#x4E00;&#x4E2A;&#x6307;&#x9488;</li><li>&#x6784;&#x9020;&#x51FD;&#x6570;&#xFF0C;&#x5B9E;&#x4F8B;&#xFF0C;&#x539F;&#x578B;&#x4E09;&#x89D2;&#x604B;&#x5173;&#x7CFB;&#x56FE;&#x8BF7;&#x79FB;&#x81F3;&#x9876;&#x90E8;</li><li>&#x83B7;&#x5F97;&#x539F;&#x578B;&#x7684;&#x65B9;&#x6CD5;<br>&#x2460;&#x6784;&#x9020;&#x51FD;&#x6570;.prototype<br>&#x2461;&#x5B9E;&#x4F8B;.__proto__<br>&#x2462;Object.getPrototypeOf()&#x65B9;&#x6CD5;&#xFF1A;&#x8BE5;&#x65B9;&#x6CD5;&#x7528;&#x4E8E;&#x83B7;&#x53D6;&#x5B9E;&#x4F8B;&#x7684;&#x539F;&#x578B;&#xFF0C;&#x6BD4;&#x8F83;&#x63A8;&#x8350;&#xFF0C;&#x56E0;&#x4E3A;&#x5927;&#x90E8;&#x5206;&#x6D4F;&#x89C8;&#x5668;&#x90FD;&#x652F;&#x6301;</li><li>isPrototypeOf()&#x65B9;&#x6CD5;&#xFF1A;&#x7528;&#x4E8E;&#x5224;&#x65AD;&#x8FD9;&#x4E2A;&#x5B9E;&#x4F8B;&#x7684;&#x6307;&#x9488;&#x662F;&#x5426;&#x6307;&#x5411;&#x8FD9;&#x4E2A;&#x539F;&#x578B;&#x3002;</li><li>delete&#x64CD;&#x4F5C;&#x7B26;&#x53EF;&#x4EE5;&#x5220;&#x9664;&#x5BF9;&#x8C61;&#x5C5E;&#x6027;&#xFF0C;&#x65E0;&#x8BBA;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#x662F;&#x5728;&#x539F;&#x578B;&#x4E0A;&#x8FD8;&#x662F;&#x5B9E;&#x4F8B;&#x4E0A;</li><li>hasOwnProperty&#x65B9;&#x6CD5;&#x7528;&#x4E8E;&#x68C0;&#x6D4B;&#x67D0;&#x4E00;&#x5C5E;&#x6027;&#x662F;&#x5426;&#x662F;&#x5BF9;&#x8C61;&#x81EA;&#x8EAB;&#x5C5E;&#x6027;&#x3002;</li><li>in&#x64CD;&#x4F5C;&#x7B26;&#x6709;&#x4E24;&#x79CD;&#x4F7F;&#x7528;&#x65B9;&#x5F0F;<br>&#x2460;for-in&#xFF1A;&#x7528;&#x4E8E;&#x904D;&#x5386;&#x5BF9;&#x8C61;&#x53EF;&#x679A;&#x4E3E;&#x5C5E;&#x6027;&#xFF0C;&#x4F1A;&#x5728;&#x539F;&#x578B;&#x4E0A;&#x641C;&#x7D22;<br>&#x2461;&#x5355;&#x72EC;&#x4F7F;&#x7528;&#xFF1A;&#x5224;&#x65AD;&#x5BF9;&#x8C61;&#x4E2D;&#x662F;&#x5426;&#x6709;&#x8FD9;&#x4E2A;&#x5C5E;&#x6027;&#xFF0C;&#x4EC5;&#x9650;&#x4E8E;&#x53EF;&#x679A;&#x4E3E;&#x5C5E;&#x6027;&#xFF0C;&#x8FD4;&#x56DE;Boolean&#x7C7B;&#x578B;</li><li>Object.keys()&#x53EA;&#x904D;&#x5386;<strong>&#x81EA;&#x8EAB;</strong>&#x7684;&#x53EF;&#x679A;&#x4E3E;&#x5C5E;&#x6027;&#xFF0C;&#x8FD4;&#x56DE;&#x4E00;&#x4E2A;&#x5C5E;&#x6027;&#x6570;&#x7EC4;</li><li>Object.getOwnPropertyNames()&#x65B9;&#x6CD5;&#xFF1A;&#x83B7;&#x53D6;<strong>&#x81EA;&#x8EAB;</strong>&#x6240;&#x6709;&#x5C5E;&#x6027;&#xFF0C;&#x65E0;&#x8BBA;&#x5B83;&#x662F;&#x5426;&#x53EF;&#x679A;&#x4E3E;</li><li>&#x6BCF;&#x521B;&#x5EFA;&#x4E00;&#x4E2A;&#x51FD;&#x6570;&#xFF0C;&#x5C31;&#x4F1A;&#x540C;&#x65F6;&#x521B;&#x5EFA;&#x5B83;&#x7684;prototype&#x5BF9;&#x8C61;&#xFF0C;&#x8FD9;&#x4E2A;&#x5BF9;&#x8C61;&#x4F1A;&#x81EA;&#x52A8;&#x83B7;&#x5F97;constructor&#x5C5E;&#x6027;&#x3002;</li><li>&#x539F;&#x578B;&#x6A21;&#x5F0F;&#x7684;&#x6700;&#x5927;&#x95EE;&#x9898;&#x662F;&#x7531;&#x5176;&#x5171;&#x4EAB;&#x672C;&#x6027;&#x6240;&#x5BFC;&#x81F4;&#x7684;</li></ul><h1>&#x5C3E;&#x58F0;</h1><p>&#x51FD;&#x6570;&#x539F;&#x578B;&#x7684;&#x63A2;&#x7D22;&#x4E4B;&#x8DEF;&#x4EFB;&#x91CD;&#x9053;&#x8FDC;&#xFF0C;&#x4E5F;&#x662F;JS&#x91CD;&#x70B9;&#x4E4B;&#x4E00;&#x3002;</p>
{{< /raw >}}

# 版权声明
本文资源来源互联网，仅供学习研究使用，版权归该资源的合法拥有者所有，

本文仅用于学习、研究和交流目的。转载请注明出处、完整链接以及原作者。 

原作者若认为本站侵犯了您的版权，请联系我们，我们会立即删除！

## 原文标题
一眼看穿👀JS原型

## 原文链接
[https://segmentfault.com/a/1190000016065038](https://segmentfault.com/a/1190000016065038)


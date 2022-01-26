JavaScript 语言的**每一个值都属于某一种数据类型**。JavaScript 语言规定了 7 种语言类型。语言类型广泛用于变量、函数参数、表达式、函数返回值等场合。根据最新的语言标准，这 7 种语言类型是：
- Undefined
- Null
- Boolean
- String
- Number
- Symbol （ES6 中新加入的类型）
- Object


- 为什么有的编程规范要求用 void 0 代替 undefined？
	Undefined类型表示未定义，只有一个值undefined。但是undefined不是关键字。。。。
	任何变量在未赋值前都是Undefined类型，值都是undefined。
	一般我们可以用全局变量 undefined（就是名为 undefined 的这个变量）来表达这个值，或者 void 运算来把任意一个表达式变成 undefined 值。

- Null 类型也只有一个值，就是 null，它的语义表示空值，与 undefined 不同，null 是 JavaScript 关键字，所以在任何代码中，你都可以放心用 null 关键字来获取 null 值。

- String 用于表示文本数据。String 有最大长度是 2^53 - 1，这在一般开发中都是够用的，但是有趣的是，**这个所谓最大长度，并不完全是你理解中的字符数**。
   因为 String 的意义并非“字符串”，而是**字符串的 UTF16 编码**，我们字符串的操作 charAt、charCodeAt、length 等方法针对的都是 **UTF16 编码**。所以，字符串的最大长度，实际上是受字符串的编码长度影响的。

- Number 类型表示我们通常意义上的“数字”。这个数字大致对应数学中的有理数，当然，在计算机中，我们有一定的精度限制。JavaScript 中的 Number 类型有 18437736874454810627(即 2^64-2^53+3) 个值。
	- JavaScript 中的 Number 类型基本符合 IEEE 754-2008 规定的双精度浮点数规则，但是 JavaScript 为了表达几个额外的语言场景（比如不让除以 0 出错，而引入了无穷大的概念），规定了几个例外情况：
		- NaN，占用了 9007199254740990，这原本是符合 IEEE 规则的数字；
		- Infinity，无穷大；
		- -Infinity，负无穷大。
	- 值得注意的是，JavaScript 中有 +0 和 -0，在加法类运算中它们没有区别，但是除法的场合则需要特别留意区分，“忘记检测除以 -0，而得到负无穷大”的情况经常会导致错误，而区分 +0 和 -0 的方式，正是检测 1/x 是 Infinity 还是 -Infinity。
	- 根据浮点数的定义，非整数的 Number 类型无法用 == （ ===  也不行） 来比较，一段著名的代码，这也正是我们第三题的问题，为什么在 JavaScript 中，0.1+0.2 不能 =0.3：
		- 0.1 + 0.2 不是等于 0.3 么？为什么 JavaScript 里不是这样的？
		- 所以实际上，这里错误的不是结论，而是比较的方法，正确的比较方法是使用 JavaScript 提供的最小精度值：
		```console.log( Math.abs(0.1 + 0.2 - 0.3) <= Number.EPSILON);```

- Symbol 是 ES6 中引入的新类型，它是一切非字符串的对象 key 的集合，在 ES6 规范中，整个对象系统被用 Symbol 重塑。

- Object 是 JavaScript 中最复杂的类型，也是 JavaScript 的核心机制之一。Object 表示对象的意思，它是一切有形和无形物体的总称。
	- JavaScript 中的“类”仅仅是运行时对象的一个私有属性，而 JavaScript 中是无法自定义类型的。

- 为什么给对象添加的方法能用在基本类型上？
	- . 运算符提供了装箱操作，它会根据基础类型构造一个临时对象，使得我们能在基础类型上调用对应对象的方法。

- JavaScript 中的“ == ”运算，因为试图实现跨类型的比较，它的规则复杂到几乎没人可以记住。它属于设计失误，并非语言中有价值的部分，很多实践中推荐禁止使用“ == ”，而要求程序员进行显式地类型转换后，用 === 比较。

- List 和 Record： 用于描述函数传参过程。
- Set：主要用于解释字符集等。
- Completion Record：用于描述异常、跳出等语句执行过程。
- Reference：用于描述对象属性访问、delete 等。
- Property Descriptor：用于描述对象的属性。
- Lexical Environment 和 Environment Record：用于描述变量和作用域。
- Data Block：用于描述二进制数据。

- 事实上，“类型”在 JavaScript 中是一个有争议的概念。一方面，标准中规定了运行时数据类型； 另一方面，JavaScript 语言中提供了 typeof 这样的运算，用来返回操作数的类型，但 typeof 的运算结果，与运行时类型的规定有很多不一致的地方。我们可以看下表来对照一下。
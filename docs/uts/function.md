## 函数（function）

函数是编程语言常见的功能，它可以封装一批代码，对外接收参数，然后返回值。被封装的逻辑，可以被不同的其他代码调用，达到共同复用逻辑的目的。

函数用 `function` 关键字定义，后面跟着函数名和圆括号。

同时注意，定义函数涉及作用域。

### 定义函数

#### 普通函数声明

一个函数定义（也称为函数声明，或函数语句）由一系列在 function 关键字后的内容组成，依次为：

-   函数的名称。
-   函数参数列表，包围在括号中并由逗号分隔。
-   函数返回值类型。
-   定义函数的 uts 语句，用大括号 `{}` 括起来。

> 注意：函数必须明确标明返回值类型

例如，以下的代码定义了一个简单的函数。函数名为 add，有2个参数 x 和 y，都是 string类型，函数的返回值类型也是 string。

函数的内容是将入参 x 和 y 相加，赋值给变量z，然后通过 return关键字返回z。

```ts
function add(x :string, y :string) :string {
    let z : string = x + " " + y
	return z;
}
```

#### 无返回值的函数定义（void）

如果这个函数不需要返回值，需要使用void关键字，同时函数内部末尾不需要return来返回内容。

```ts
function add(x :string, y :string) :void {
    let z :string = x + " " + y
	console.log(z)
	// 不需要return
}
```

#### 函数表达式和匿名函数定义

虽然上面的函数声明在语法上是一个语句，但函数也可以由函数表达式创建。这样的函数可以是匿名的，它不必有一个名称。例如，函数 add 也可这样来定义：

```ts
const add = function (x: string, y: string): string {
    return x + " " + y;
};
```

注意：
- 通过表达式定义的函数必须使用return关键字返回内容。
- 函数表达式不支持使用函数名，比如`const add = function add(){}`是不允许的。

### 调用函数

定义一个函数并不会自动的执行它。定义了函数仅仅是赋予函数以名称并明确函数被调用时该做些什么。调用函数才会以给定的参数真正执行这些动作。

定义了函数 add 后，你可以如下这样调用它：

```ts
function add(x :string, y :string) :string {
    let z :string = x + " " + y
	return z;
}
add("hello", "world"); // 调用add函数
```

上述语句通过提供参数 "hello" 和 "world" 来调用函数。

虽然调用了add函数，但并没有获取到返回值。如需要获取返回值，需要再赋值：
```ts
function add(x :string, y :string) :string {
	let z :string = x + " " + y
	return z;
}
let s :string = add("hello", "world");
console.log(s) // hello world
```

### 函数作用域

在函数内定义的变量不能在函数之外的任何地方访问，因为变量仅仅在该函数的域的内部有定义。相对应的，一个函数可以访问定义在其范围内的任何变量和函数。

```ts
const hello :string = "hello";
const world :string = "world";

function add(): string {
	let s1 :string = "123";
    return hello + world; // 可以访问到 hello 和 world
}
```

#### 嵌套函数

你可以在一个函数里面嵌套另外一个函数。嵌套（内部）函数对其容器（外部）函数是私有的。它自身也形成了一个闭包。一个闭包是一个可以自己拥有独立的环境与变量的表达式（通常是函数）。

既然嵌套函数是一个闭包，就意味着一个嵌套函数可以”继承“容器函数的参数和变量。换句话说，内部函数包含外部函数的作用域。

可以总结如下：

-   内部函数只可以在外部函数中访问。
-   内部函数形成了一个闭包：它可以访问外部函数的参数和变量，但是外部函数却不能使用它的参数和变量。

举例：

```ts
function addSquares(a: number, b: number): number {
    function square(x: number): number {
        return x * x;
    }
    return square(a) + square(b);
}
addSquares(2, 3); // returns 13
addSquares(3, 4); // returns 25
addSquares(4, 5); // returns 41
```

#### 命名冲突

当同一个闭包作用域下两个参数或者变量同名时，就会产生命名冲突。更近的作用域有更高的优先权，所以最近的优先级最高，最远的优先级最低。这就是作用域链。链的第一个元素就是最里面的作用域，最后一个元素便是最外层的作用域。

举例：

```ts
function outside(): (x: number) => number {
    let x = 5;
    const inside = function (x: number): number {
        return x * 2;
    };
    return inside;
}

outside()(10); // 返回值为 20 而不是 10
```

命名冲突发生在 `return x` 上，inside 的参数 x 和 outside 变量 x 发生了冲突。这里的作用链域是 `{inside, outside}`。因此 inside 的 x 具有最高优先权，返回了 20（inside 的 x）而不是 10（outside 的 x）。

### 闭包

uts 允许函数嵌套，并且内部函数可以访问定义在外部函数中的所有变量和函数，以及外部函数能访问的所有变量和函数。

但是，外部函数却不能够访问定义在内部函数中的变量和函数。这给内部函数的变量提供了一定的安全性。

此外，由于内部函数可以访问外部函数的作用域，因此当内部函数生存周期大于外部函数时，外部函数中定义的变量和函数的生存周期将比内部函数执行时间长。当内部函数以某一种方式被任何一个外部函数作用域访问时，一个闭包就产生了。

举例：

```ts
const pet = function (name: string): () => string {
    //外部函数定义了一个变量"name"
    const getName = function (): string {
        //内部函数可以访问 外部函数定义的"name"
        return name;
    };
    //返回这个内部函数，从而将其暴露在外部函数作用域
    return getName;
};
const myPet = pet("Vivie");
myPet(); // 返回结果 "Vivie"
```

### 函数参数

#### 默认参数

函数参数可以有默认值，当省略相应的参数时使用默认值。

```ts
function multiply(a:number, b:number = 1):number {
  return a*b;
}
multiply(5); // 5
```
### 箭头函数

箭头函数表达式（也称胖箭头函数）相比函数表达式具有较短的语法。箭头函数总是匿名的。

```ts
const arr = ["Hydrogen", "Helium", "Lithium", "Beryllium"];
const a2 = arr.map(function (s): number {
    return s.length;
});
console.log(a2); // logs [ 8, 6, 7, 9 ]
const a3 = arr.map((s): number => s.length);
console.log(a3); // logs [ 8, 6, 7, 9 ]
```
## 12个必备的JavaScript装逼技巧(转发)

----------

在这里我把使用多年的奇淫技巧给大家分享出来，教大家写出更加简洁的代码。

### 1. 空(null, undefined)验证

当我们创建了一个新的变量，我们通常会去验证该变量的值是否为空(null)或则未定义(undefined)。这对于JavaScript编程来说，是一个经常要考虑到的验证。

如果直接写，那么像下面这样：

if (variable1 !== null || variable1 !== undefined || variable1 !== '') { let variable2 = variable1; }
我们可以使用一个更加简洁的版本：

let variable2 = variable1  || '';
如果你不信，在谷歌浏览器开发者面板的控制台下试试！

//值为null的例子
<blockquote>let variable1 = null;
let variable2 = variable1  || '';
console.log(variable2);
//输出: '' 
//值为undefined的例子
let variable1 = undefined;
let variable2 = variable1  || '';
console.log(variable2);
//输出: '' 
//正常情况
let variable1 = 'hi there';
let variable2 = variable1  || '';
console.log(variable2);
//输出: 'hi there'
</blockquote>

### 2. 数组

这个好像比较简单！
非优化代码：

let a = new Array(); a[0] = "myString1"; a[1] = "myString2"; a[2] = "myString3";
优化代码：

let a = ["myString1", "myString2", "myString3"];

### 3. if true .. else 的优化

let big;
if (x > 10) {
    big = true;
}
else {
    big = false;
}
简化后：

let big = x > 10 ? true : false;
极大简化了代码量！

let big = (x > 10);
let x = 3,
big = (x > 10) ? "greater 10" : (x < 5) ? "less 5" : "between 5 and 10";
console.log(big); //"less 5"
let x = 20,
big = {true: x>10, false : x< =10};
console.log(big); //"Object {true=true, false=false}"

### 4. 变量声明

尽管JavaScript会自动将变量上提(hoist)，使用该方法可以将所有的变量都在函数的头部用一行搞定。

优化前：

let x;
let y;
let z = 3;
优化后：

let x, y, z=3;

### 5. 赋值语句的简化

简化前：

x=x+1;
minusCount = minusCount - 1;
y=y*10;
简化后：

x++;
minusCount --;
y*=10;
假设 x=10，y=5，那么基本的算术操作可以使用如下的简写方式：

x += y // x=15
x -= y // x=5
x *= y // x=50
x /= y // x=2
x %= y // x=0

### 6. 避免使用RegExp对象

简化前：

var re = new RegExp("\d+(.)+\d+","igm"),
result = re.exec("padding 01234 text text 56789 padding");
console.log(result); //"01234 text text 56789"
简化后：

var result = /d+(.)+d+/igm.exec("padding 01234 text text 56789 padding");
console.log(result); //"01234 text text 56789"

### 7. If 条件优化

虽然很简单，但还是值得提一下。

简化前：

if (likeJavaScript === true)
简化后：

if (likeJavaScript)
我们再来句一个判断非真的例子：

let c;
if ( c!= true ) {
// do something...
}
简化后：

let c;
if ( !c ) {
// do something...
}

### 9. 函数参数优化

我个人倾向于使用获取对象元素的方式来访问函数参数，当然这个见仁见智啦！

通常使用的版本：

function myFunction( myString, myNumber, myObject, myArray, myBoolean ) {
    // do something...
}
myFunction( "String", 1, [], {}, true );
我喜欢的版本：

function myFunction() {
    /* 注释部分
    console.log( arguments.length ); // 返回 5
    for ( i = 0; i < arguments.length; i++ ) {
        console.log( typeof arguments[i] ); // 返回 string, number, object, object, boolean
    }
    */
}
myFunction( "String", 1, [], {}, true );
译者注：原文下方有评论表示不建议用楼主的方法，使用第一种方法函数参数的顺序是可以变动的，第二种你就要小心了。

### 10. charAt()的替代品

简化前：

"myString".charAt(0);
简化后：

"myString"[0]; // 返回 'm'
译者注：我相信用第一种方法的人已经不多了吧！

### 11. 函数调用还可以更短

简化前：

function x() {console.log('x')};function y() {console.log('y')};
let z = 3;
if (z == 3) 
{
    x();
} else 
{
    y();
}
简化后：

function x() {console.log('x')};function y() {console.log('y')};let z = 3;
(z==3?x:y)();
你说四不四很短？

### 12. 如何优雅的表示大数字

在JavaScript中，有一个简写数字的方法，也许你忽略了。1e7表示10000000。

简化前：

for (let i = 0; i < 10000; i++) {
简化后：

for (let i = 0; i < 1e7; i++) {

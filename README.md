# ES6 笔记

ES6学习笔记

> 注：由于记录此笔记时我主要使用 Swift 语言进行开发，则文中对于此时我比较混淆的地方会用 Swift 进行类比。
>> 其它语言的比对或补充望同样在学习ES6的小伙伴也能够列举出来，提交给我，我会review内容并合并，方便一起学习！

## 目 录
* [**var let const**](#var-let-const)

## var let const

* **var let 区别**

  var 在以下这样的代码块里依然是全局变量，但是 let 在里面是局部变量。
  
  ```js
  {
      var a = 1;
      let b = 2;
  }
  //输出: 1
  console.log(a);
  // 报错！
  console.log(b);
  ```
  
  在 function 里面，var 和 let 则都不可取到，其声明都是以局部变量呈现，在我看来它们都是一样的。
  
  ```js
  function func() {
      var a = 1;
      a = 3;
      //输出 3
      console.log(a);
      let b = 2;
      b = 4;
      //输出 4
      console.log(b);
  }
  func();
  // 报错！
  console.log(a);
  // 报错！
  console.log(b);
  ```
  
  且 var 命令存在 “变量提升”，也就是只要用 var 定义了变量，就算是在声明之前引用它，都不会报错；但是对 let 来说，它就很安全了，在定义之前的引用，都会报错！
  
  ```js
  //undefined
  console.log(a);
  var a = 1;

  // 报错！
  console.log(b);
  let b = 1;
  ```
  
  **总结：**现在我还不知道多文件全局变量中怎么声明，但是在单文件中，一个 let 声明就足够了！只要在代码块里，let 就是无敌的，在代码块外，let 什么都不是。

* **const**

  它就是声明常量用的，注意规范：**常量全部用大些字母表示**。
  
  ```js
  const PI = 3.14159;
  // 报错！
  PI = "what?";
  ```
  
  但是 const 也仅仅能保证
  
* **对比语言**
  * **Swift**

     在 Swift 中声明变量的方法只有 var 属性，这个 var 在单文件中，其作用就是ES6中的 let ！
         
     而 ES6 中的 const，则是声明常量的方法，作用和 Swift 里的 let 一摸一样。

## 解构赋值

* 什么是解构赋值？


---
title: codewars 题目记录
date: 2018-01-29 15:40:37
categories: codewars
---

### codewars题目（拆房子）：  
Your task is to construct a building which will be a pile of n cubes. The cube at the bottom will have a volume of n^3, the cube above will have volume of (n-1)^3 and so on until the top which will have a volume of 1^3.

You are given the total volume m of the building. Being given m can you find the number n of cubes you will have to build?

The parameter of the function findNb `(find_nb, find-nb, findNb)` will be an integer m and you have to return the integer n such as n^3 + (n-1)^3 + ... + 1^3 = m if such a n exists or -1 if there is no such n.

google翻译：   
你的任务是建造一个将是一堆n个立方体的建筑物。底部的立方体的体积为n ^ 3，上面的立方体的体积为（n-1）^ 3等等，直到顶部的体积为1 ^ 3。  

你得到建筑物的总体积m。被赋予m可以找到你需要建立的立方体的数量n吗？  

函数findNb（find_nb，find-nb，findNb）的参数是一个整数m，必须返回整数n，如n ^ 3 +（n-1）^ 3 + ... + 1 ^ 3 =如果存在，则为-1;如果不存在，则为-1。

Test.describe("Basic tests",function() {

Test.assertEquals(findNb(4183059834009), 2022)  
Test.assertEquals(findNb(24723578342962), -1)  
Test.assertEquals(findNb(135440716410000), 4824)  
Test.assertEquals(findNb(40539911473216), 3568)  
})

解题思路：从最上面一层往下拆、直到m == 0 的时候就刚好拆完了、如果m < 0的时候就返回-1

代码如下： 

```
function findNb(m) {
    // your code
  for (var i = 1; i < m; i ++) {
    m = m - i*i*i
  }
  if (m === 0) {
      return i - 1
    } else {
      return -1
    }
}
```


### 求从1到给定数字之间所有数的和：  
前提： 假设num总是大于0

```
function summation(num) {
  return num * (num + 1) / 2
}
```

### 找出数组中某一字符串的位置：
找出needle的位置

```
function findNeedle(haystack) {
  return "found the needle at position " + haystack.indexOf("needle");
}
```

### Growth of a Population(人口增长)：
**描述：**  
In a small town the population is p0 = 1000 at the beginning of a year. The population regularly increases by 2 percent per year and moreover 50 new inhabitants per year come to live in the town. How many years does the town need to see its population greater or equal to p = 1200 inhabitants?  

在一个小镇，一年初的人口是p0 = 1000。人口每年定期增长2％，而且每年有50名新居民来到这个城镇居住。该镇需要多少年才能看到其人口大于或等于p = 1200的居民？（来自google翻译）

```
p0：原始人口数, 
percent：每年增长人数的速率, 
aug：每年新定居或离开人数, 
p：需要到达的人口数
```

代码如下：

```
function nbYear(p0, percent, aug, p) {
        // your code
        var i = 0;
        while(p0 < p) {
          p0 = p0 + p0 * percent / 100 + aug;
          i++;
        }
        return i
      }
```


### 翻转字符串：

```
var x = "qwer";
return x.split("").reverse().join("");
```

### 正则表达式：

```
var x = '\djI38D55';
console.log(/^(?=.*[0-9])(?=.*[a-z])(?=.*[A-Z])(?!.*[.~!@#$%^&* _+|<>?:";'/])).{6,}/.test(x));

(?=.*[0-9])：必须包含数字
(?=.*[a-z])(?=.*[A-Z])：必须包含大小写字母
(?!.*[.~!@#$%^&* _+|<>?:";'/])：不能包含这些特殊字符包括空格
{6,}：最小长度为6  逗号后面无值表示最大长度无限制
```

### Sum of the first nth term of Series（这个系列的第一个第n期）：

`Series: 1 + 1/4 + 1/7 + 1/10 + 1/13 + 1/16 +...`

**Examples:**

```
SeriesSum(1) => 1 = "1.00"
SeriesSum(2) => 1 + 1/4 = "1.25"  
SeriesSum(5) => 1 + 1/4 + 1/7 + 1/10 + 1/13 = "1.57"
```

**Code:**

```
function SeriesSum(n) {
  var sum = 0;
  for(var i = 0; i < n; i++) {
    sum += 1 / (3 * i + 1);
  }
  return sum.toFixed(2);
}
```
or

```
function SeriesSum(n) {
  var sum = 0;
  for(var i = 0; i < 3*n-2; i++) {
    sum += 1/i;
  }
  return sum.toFixed(2);
}
```

### Replace With Alphabet Position(替换为字母表位置)

**description：**  
given a string, replace every letter with its position in the alphabet.（给定一个字符串，用字母表中的位置替换每个字母。）


```
function alphabetPosition(text) {
  var A_Z="";
      var arr = [];
      var arr1 = [];
      text = text.split('');
      for(var i=65;i<91;i++)
      // 利用Unicode编码来循环出26个大学的英文字母
      {
        A_Z+=String.fromCharCode(i)+" ";  // 转换Unicode编码
      }
      arr = A_Z.split(' ');  // 将英文字母变成数组
      arr.pop();		// 删掉最后的一个空格
      for (var j = 0; j < text.length; j++) {
        for (var k = 0; k < arr.length; k++) {
          if (text[j].toLowerCase() === arr[k].toLowerCase()) {  // 将字母都变成小写的再进行比较
            arr1.push(k+1);
          }
        }
      }
      return arr1.join(" ");
}
```

### Money, Money, Money：

**description：** 
存钱到银行、多少年才能到达期望的金额

principal：本金  
interest：利息  
tax：税率  
desired：期望达到的金额  

**要点：**
首先要知道这个公式是啥样儿的。  

本金 + 本金 * 利息 * （1 - 税率）* 年数 > 期望达到的金额

**code：**

```
function calculateYears(principal, interest, tax, desired) {
    // your code
      var y = 0;
      if (principal < desired) {
      while (principal <= desired) {
        principal += principal * interest * (1 - tax);
        y++;
      }
      } else {
        return 0
      }
      return y;
}
```

### IQ Test：

**Examples :**

```
iqTest("2 4 7 8 10") => 3 // Third number is odd, while the rest of the numbers are even

iqTest("1 2 1 1") => 2 // Second number is even, while the rest of the numbers are odd
```

**Code:**
 
```
function iqTest(numbers){
  // ...
  var arr = numbers.split(' ');
  var odd = [], even = [];
      for (var i = 0; i < arr.length; i++) {
        if (arr[i]%2 === 0) {
          odd.push(i);
        } else {
          even.push(i);
        }
      }
      if (odd.length > even.length) {
        return even[0] + 1;
      } else {
        return odd[0] + 1;
      }
}
```

### Sum of numbers from 0 to N：

**Description：**  
给定一个整数count、输出从0到count的和、并且带上加的过程。

**Example:**  
Input：count = 6;  
Output：`0+1+2+3+4+5+6 = 21`

Input：count = -15;  
Output：`-15<0`

Input：count = 0;  
Output：`0=0`

code：

```
var i = 0, a = 0, x = 0, b, c, z;
      if (count == 0) {
        return '0=0';
      } else if (count < 0) {
	   	  return count + '<0';
	   }      
      {
        while (i <= count) {
          x+=i;
          a += '+' + i.toString();
          i++;
        }
        b = a.split('+');
        b.shift();
        c = b.join('+');
        z = c + ' ' + '=' + ' ' + x;
        return z;
      }
```

大牛的答案：

```
return n < 0
        ? `${n}<0`
        : `${Array.from({length: n+1}, (v, k) => k).join('+')}${n?' = ':'='}${n*(n+1)/2}`;
```
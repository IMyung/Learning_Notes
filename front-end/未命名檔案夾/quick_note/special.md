**JS Comparison**

Given that x = 5  ( number )
```JS
===	equal value and equal type

x   ===     5	    true	
x   ===    "5"	    false
```

```JS
!==	not equal value or not equal type

x   !==     5	    false	
x   !==    "5"	    true	
x   !==     8	    true
```

```JS
邏輯運算子

Logical Operators   ： &&  ||  !
conditional operator：（condition） ? :
```

```JavaScript
Comparing Different Types
比較不同類型可能會造成不預期的結果
所以在比較前一定要進行型態轉換

當字串和數字比較, JS 會把字串轉成數字進行比較
一個空字串會轉化成 0 值
非數值字串會轉成 NaN 並總是會造成 false

 2   <     12	    true	
 2   <    "12"	    true	
 2   <   "John"	    false	
 2   >   "John"	    false	
 2   ==  "John"	    false	
"2"  <    "12"	    false	 <<  不預期
"2"  >    "12"	    true	 << 
"2"  ==   "12"	    false	 

```
---

**JS condition**
完全一樣

---

**JS switch**

```JS
switch(expression) {
  case x:
    ...
    break;
  
  case y:
  case z:
    ...
    break;
  
  dafault :
    ...
}
```

**JS For loop**

JS 有四種迴圈
```JS
for ( s1 ; s2 ; s3 ) {
    ...
}

可以在 s1 當中，以逗號隔開，初始多個變數
```

```JS
The For/In Loop
遍歷一個 object 

var person = {fname:"John", lname:"Doe", age:25}; 

var text = "";
var x;
for (x in person) {
  text += person[x];
}
```

---

**JS while**
一致

---



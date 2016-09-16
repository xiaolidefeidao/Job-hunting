##### 在HTML5中，提供了强大的DOM元素选择API querySelector/querySelectorAll，允许使用JavaScript代码来完成类似CSS选择器的DOM元素选择功能。通常情况下，我们都是使用的document.querySelector/querySelectorAll来选择DOM元素，但是有些时候会使用DOM元素上的querySelector/querySelectorAll方法，此时就有些怪异了。
比如说，下面的这样一个HTML页面（示例页面中为了方面说明问题，我为每个元素都加上了ID，但是我们不使用ID选择器来选择元素）：

 ```html
 <body>
      <span id="s0">This is a span direct child of body</span>
      <div id="d1" style="border: 1px solid red;">
          This is div d1
          <div id="d1-1" style="border: 1px solid blue;">
              This is div d1-1 <br/>
              <span id="d1-1-1">This span d1-1-1</span> 
          </div>
         <span id="d1-2">This is span d1-2</span>
     </div>
 </body>
 ```
在这个场景中，元素div#d1有2个子元素，分别是div#d1-1和span#d1-2，而元素div#d1-1有一个span#div-1-1-1的子元素。如果我想从div#d1上选择span#d1-1-1，如果使用子元素选择器的话，在jQuery中看起来应该是这样的：

$("#d1").find("div > span")
这段代码会返回span#d1-1-1，就是我们预期的结果。

那么对应到HTML5中的选择器API就应该是这样写的：
var d1 = document.querySelector("#d1");
var spans = d1.querySelectorAll("div > span");
你期望上面这段代码会返回span#d1-1-1，但是实际上的运行结果会连同span#d1-1一并返回！
```html
[<span id="d1-1-1">This span d1-1-1</span>,<span id="d1-2">This is span d1-2</span>]
```
当在一个DOM元素上调用querySelector/querySelectorAll的时候，查找机制是这样的：
+ 首先在document的范围内进行查找所有满足选择器条件的元素，在上面这段代码中，我们的选择器是div > span，就是所有的直接父元素为div的span元素。
+ 再看哪些元素是调用querySelector/querySelectorAll的元素的子元素，这些元素将会被返回。这也就说明了为什么d1.querySelectorAll("div > span") 会连同span#d1-2一并返回。
所以，在DOM元素上调用querySelector/querySelectorAll的时候要小心，最好加上ID选择器进行一个限定，例如上面的代码可以写成：
d1.querySelectorAll("#d1 > div > span");

## js中的&&和||本质上是求boolean值

* &&：若整个表达式值为true,返回最后一个子表达式的结果；<br/>
      若整个表达式值为false,返回第一个boolean值为false的子表达式的结果；<br/>
      *即：返回第一个boolean为false的子表达式，否则返回最后一个子表达式*

* ||：若整个表达式值为true,返回第一个boolean值为true的子表达式的结果；<br/>
      若整个表达式值为false,返回最后一个子表达式的结果；<br/>
      *即：返回第一个boolean为true的子表达式，否则返回最后一个子表达式*
#### null undefined NaN "" 0  这些数据在逻辑运算中都会判为false

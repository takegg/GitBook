# Arrow_Functions

##### 使用了块语句的箭头函数不会自动返回值，你需要使用return语句将所需值返回。
```js
    $("#confetti-btn").click(event => {
      return fu();
    });
```
或这样return
```js
    $("#confetti-btn").click(event => 
      fu();
```

##### 创建普通对象时，需将对象包裹在小括号里
```js
var chewToys = puppies.map(puppy => ({}));
```

##### 无this值，箭头函数内的this值继承自外围作用域
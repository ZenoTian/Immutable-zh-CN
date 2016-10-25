## is()

语法与`Object.is`类似，用来判断两个值是否相等，但是对于Immutable，会判断两个`Iterable`（可迭代）所包含的值是否相等

> is(first: any, second: any): boolean

##### 讨论

当用来判断Immutable是否相等的时候，也会判断`Map`的键和`Set`的成员。

```javascript
var map1 = Immutable.Map({a:1, b:1, c:1});
var map2 = Immutable.Map({a:1, b:1, c:1});
assert(map1 !== map2);
assert(Object.is(map1, map2) === false);
assert(Immutable.is(map1, map2) === true);
```

`Object.is`类似于`===`判断两个对象是不是同一个，而`Immutable.is`判断的两个对象内每个键与值是否相等

注意：与`Object.is`不同，`Immutable.is`假设`0` 和`-0`是相同的，这和ES6 Map的键行为一样。


# formJS\(\)

将原生JS的对象和数组进行深度转换，转换为Immutable的Map和List

```javascript
fromJS(json: any, reviver?: (k: any, v: Iterable<any, any>) => any): any
```

如果`reviver`这个属性被提供了，那么它会传入一个Seq对象并且被循环调用，对于顶层对象，它的默认的键为`""`。

`Immutable.fromJS`进行的转换是保守的。他只会将`Array.isArray`返回结果为true的数组转换为List,将原生的对象（非自定义的原型）转换为Map。

请注意，当使用JS对象生成Immutable的Map，JavaScript Object属性始终是字符串，即使使用数字作为键，而Immutable的Map类型接受任何类型的键

```javascript
var obj = { 1: "one" };
Object.keys(obj); // [ "1" ]
obj["1"]; // "one"
obj[1];   // "one"

var map = Map(obj);
map.get("1"); // "one"
map.get(1);   // undefined
```

访问JavaScript对象会首先将键转化成为string类型，但是Immutable的Map的键可以是任何类型的，
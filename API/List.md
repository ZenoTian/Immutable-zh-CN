## List

List是根据索引紧密排序的集合，就像JavaScript数组。

> class List<T> extends [Collection.Indexed](https://facebook.github.io/immutable-js/docs/#/Collection.Indexed)<T>

##### List()

创建一个新的包含可迭代的值的Immutable List。

>List<T>(): [List](https://facebook.github.io/immutable-js/docs/#/List)<T>
>List<T>(iter: [Iterable.Indexed](https://facebook.github.io/immutable-js/docs/#/Iterable.Indexed)<T>): [List](https://facebook.github.io/immutable-js/docs/#/List)<T>
>List<T>(iter: [Iterable.Set](https://facebook.github.io/immutable-js/docs/#/Iterable.Set)<T>): [List](https://facebook.github.io/immutable-js/docs/#/List)<T>
>List<K, V>(iter: [Iterable.Keyed](https://facebook.github.io/immutable-js/docs/#/Iterable.Keyed)<K, V>): [List](https://facebook.github.io/immutable-js/docs/#/List)<any>
>List<T>(array: Array<T>): [List](https://facebook.github.io/immutable-js/docs/#/List)<T>
>List<T>(iterator: Iterator<T>): [List](https://facebook.github.io/immutable-js/docs/#/List)<T>
>List<T>(iterable: Object): [List](https://facebook.github.io/immutable-js/docs/#/List)<T>

#### 静态方法

##### List.isList()

如果是List类型返回true。

> List.isList(maybeList: any): boolean

##### List()

创建一个包含`values`的List。

> List.of<T>(...values: T[]): [List](https://facebook.github.io/immutable-js/docs/#/List)<T>

#### 成员/属性

size

> size: number	

继承自

[Collection#size](https://facebook.github.io/immutable-js/docs/#/Collection/size)

##### set()

返回一个新的List,包含`value`与对应的`index`。如果`index`在名单中已经存在，将会被替换。

> set(index: number, value: T): [List](https://facebook.github.io/immutable-js/docs/#/List)<T>

`index`可以是负数，表示从List的末尾开始向前。`v.set(-1, "value")`设置List的最后一项。

如果`index`大于`size`，返回的List的`size`将会大到足够包含`index`。

##### delete()

返回一个新的List，不包含这个`index`并且比原来的List的size小1。

###### **别名**

`remove()`

###### **讨论**

与`list.splice(index, 1)`同义

`index`可能是负数,当时负数的时候表示从List的末尾开始。`v.delete(-1)` 删除List中的最后一项.。

注意：`delete`不兼容IE8

##### insert()

在List中`index`位置插入一个`value`，返回一个新的List，新的List的size比原来大1。索引比`index`大的值，索引全部增加1。

> insert(index: number, value: T): List<T>

###### **讨论**

相当于 `list.splice(index, 0, value)`的代名词。

##### clear()

返回一个没有值size为0的新的List。

> clear(): List<T>

##### push()

向数组的末尾添加一个或更多`value`，并返回新的List

> push(...values: T[]): List<T>

##### pop()

删除List的最后一个元素，返回一个比原Lise的size小1新的List，

> pop(): List<T>

###### DISCUSSION

注意：这和 `Array#pop`不同， 因为返回的是新的List而不是被删除的值。 使用 `last()`能够获得List的最后一个值。

##### unshift()

向数组的开头添加一个或更多元素，并返回新的List。

```
unshift(...values: T[]): List<T>
```

##### shift()

删除数组的第一个元素，返回一个新的List

```
shift(): List<T>
```

###### DISCUSSION

注意：和 `Array#shift`不同，因为返回的是新的List而不是被删除的值，使用`first()`能够获得List的第一个值。

### update()

Returns a new List with an updated value at `index` with the return value of calling`updater` with the existing value, or `notSetValue` if `index` was not set. If called with a single argument, `updater` is called with the List itself.

```
update(updater: (value: List<T>) => List<T>): List<T>
update(index: number, updater: (value: T) => T): List<T>
update(index: number, notSetValue: T, updater: (value: T) => T): List<T>

```

#### SEE

`Map#update`

#### DISCUSSION

`index` may be a negative number, which indexes back from the end of the List.`v.update(-1)` updates the last item in the List.

### merge()

`merge(...iterables: Iterable.Indexed[]): Listmerge(...iterables: Array[]): List`SEE`Map#merge`

### mergeWith()

`mergeWith(merger: (previous?: T, next?: T, key?: number) => T,...iterables: Iterable.Indexed[]): List
mergeWith(merger: (previous?: T, next?: T, key?: number) => T,...iterables: Array[]): List
`SEE`Map#mergeWith`

### mergeDeep()

`mergeDeep(...iterables: Iterable.Indexed[]): ListmergeDeep(...iterables: Array[]): List`SEE`Map#mergeDeep`

### mergeDeepWith()

`mergeDeepWith(merger: (previous?: T, next?: T, key?: number) => T,...iterables: Iterable.Indexed[]): List
mergeDeepWith(merger: (previous?: T, next?: T, key?: number) => T,...iterables: Array[]): List
`SEE`Map#mergeDeepWith`

### setSize()

Returns a new List with size `size`. If `size` is less than this List's size, the new List will exclude values at the higher indices. If `size` is greater than this List's size, the new List will have undefined values for the newly available indices.

```
setSize(size: number): List<T>

```

#### DISCUSSION

When building a new List and the final size is known up front, `setSize` used in conjunction with `withMutations` may result in the more performant construction.

#### Deep persistent changes

### setIn()

Returns a new List having set `value` at this `keyPath`. If any keys in `keyPath` do not exist, a new immutable Map will be created at that key.

```
setIn(keyPath: Array<any>, value: any): List<T>
setIn(keyPath: Iterable<any, any>, value: any): List<T>

```

#### DISCUSSION

Index numbers are used as keys to determine the path to follow in the List.

### deleteIn()

Returns a new List having removed the value at this `keyPath`. If any keys in `keyPath`do not exist, no change will occur.

```
deleteIn(keyPath: Array<any>): List<T>
deleteIn(keyPath: Iterable<any, any>): List<T>

```

#### ALIAS

```
removeIn()
```

### updateIn()

`updateIn(keyPath: Array, updater: (value: any) => any): List
updateIn(keyPath: Array,notSetValue: any,updater: (value: any) => any): List
updateIn(keyPath: Iterable, updater: (value: any) => any): List
updateIn(keyPath: Iterable,notSetValue: any,updater: (value: any) => any): List
`SEE`Map#updateIn`

### mergeIn()

`mergeIn(keyPath: Iterable,...iterables: Iterable.Indexed[]): List
mergeIn(keyPath: Array, ...iterables: Iterable.Indexed[]): List
mergeIn(keyPath: Array, ...iterables: Array[]): List
`SEE`Map#mergeIn`

### mergeDeepIn()

`mergeDeepIn(keyPath: Iterable,...iterables: Iterable.Indexed[]): List
mergeDeepIn(keyPath: Array, ...iterables: Iterable.Indexed[]): List
mergeDeepIn(keyPath: Array, ...iterables: Array[]): List
`SEE`Map#mergeDeepIn`

#### Transient changes

### withMutations()

Note: Not all methods can be used on a mutable collection or within `withMutations`! Only `set`, `push`, `pop`, `shift`, `unshift` and `merge` may be used mutatively.

```
withMutations(mutator: (mutable: List<T>) => any): List<T>

```

#### SEE

`Map#withMutations`

### asMutable()

`asMutable(): List`SEE`Map#asMutable`

### asImmutable()

`asImmutable(): List`SEE`Map#asImmutable`

#### Conversion to Seq

### toSeq()

Returns Seq.Indexed.

```
toSeq(): Seq.Indexed<T>

```

#### INHERITED FROM

```
Collection.Indexed#toSeq
```

### toKeyedSeq()

Returns a Seq.Keyed from this Iterable where indices are treated as keys.

```
toKeyedSeq(): Seq.Keyed<number, T>

```

#### INHERITED FROM

```
Iterable#toKeyedSeq
```

#### DISCUSSION

This is useful if you want to operate on an Iterable.Indexed and preserve the [index, value] pairs.

The returned Seq will have identical iteration order as this Iterable.

Example:

```
var indexedSeq = Immutable.Seq.of('A', 'B', 'C');
indexedSeq.filter(v => v === 'B').toString() // Seq [ 'B' ]
var keyedSeq = indexedSeq.toKeyedSeq();
keyedSeq.filter(v => v === 'B').toString() // Seq { 1: 'B' }
```

### toIndexedSeq()

Returns an Seq.Indexed of the values of this Iterable, discarding keys.

```
toIndexedSeq(): Seq.Indexed<T>

```

#### INHERITED FROM

```
Iterable#toIndexedSeq
```

### toSetSeq()

Returns a Seq.Set of the values of this Iterable, discarding keys.

```
toSetSeq(): Seq.Set<T>

```

#### INHERITED FROM

```
Iterable#toSetSeq
```

### fromEntrySeq()

If this is an iterable of [key, value] entry tuples, it will return a Seq.Keyed of those entries.

```
fromEntrySeq(): Seq.Keyed<any, any>

```

#### INHERITED FROM

```
Iterable.Indexed#fromEntrySeq
```

#### Value equality

### equals()

True if this and the other Iterable have value equality, as defined by `Immutable.is()`.

```
equals(other: Iterable<number, T>): boolean

```

#### INHERITED FROM

```
Iterable#equals
```

#### DISCUSSION

Note: This is equivalent to `Immutable.is(this, other)`, but provided to allow for chained expressions.

### hashCode()

Computes and returns the hashed identity for this Iterable.

```
hashCode(): number

```

#### INHERITED FROM

```
Iterable#hashCode
```

#### DISCUSSION

The `hashCode` of an Iterable is used to determine potential equality, and is used when adding this to a `Set` or as a key in a `Map`, enabling lookup via a different instance.

```
var a = List.of(1, 2, 3);
var b = List.of(1, 2, 3);
assert(a !== b); // different instances
var set = Set.of(a);
assert(set.has(b) === true);
```

If two values have the same `hashCode`, they are [not guaranteed to be equal](http://en.wikipedia.org/wiki/Collision_(computer_science)). If two values have different `hashCode`s, they must not be equal.

#### Reading values

### get()

Returns the value associated with the provided key, or notSetValue if the Iterable does not contain this key.

```
get(key: number, notSetValue?: T): T

```

#### INHERITED FROM

```
Iterable#get
```

#### DISCUSSION

Note: it is possible a key may be associated with an `undefined` value, so if`notSetValue` is not provided and this method returns `undefined`, that does not guarantee the key was not found.

### has()

True if a key exists within this `Iterable`, using `Immutable.is` to determine equality

```
has(key: number): boolean

```

#### INHERITED FROM

```
Iterable#has
```

### includes()

True if a value exists within this `Iterable`, using `Immutable.is` to determine equality

```
includes(value: T): boolean

```

#### INHERITED FROM

```
Iterable#includes
```

#### ALIAS

```
contains()
```

### first()

The first value in the Iterable.

```
first(): T

```

#### INHERITED FROM

```
Iterable#first
```

### last()

The last value in the Iterable.

```
last(): T

```

#### INHERITED FROM

```
Iterable#last
```

#### Reading deep values

### getIn()

Returns the value found by following a path of keys or indices through nested Iterables.

```
getIn(searchKeyPath: Array<any>, notSetValue?: any): any
getIn(searchKeyPath: Iterable<any, any>, notSetValue?: any): any

```

#### INHERITED FROM

```
Iterable#getIn
```

### hasIn()

True if the result of following a path of keys or indices through nested Iterables results in a set value.

```
hasIn(searchKeyPath: Array<any>): boolean
hasIn(searchKeyPath: Iterable<any, any>): boolean

```

#### INHERITED FROM

```
Iterable#hasIn
```

#### Conversion to JavaScript types

### toJS()

Deeply converts this Iterable to equivalent JS.

```
toJS(): any

```

#### INHERITED FROM

```
Iterable#toJS
```

#### ALIAS

```
toJSON()
```

#### DISCUSSION

`Iterable.Indexeds`, and `Iterable.Sets` become Arrays, while `Iterable.Keyeds`become Objects.

### toArray()

Shallowly converts this iterable to an Array, discarding keys.

```
toArray(): Array<T>

```

#### INHERITED FROM

```
Iterable#toArray
```

### toObject()

Shallowly converts this Iterable to an Object.

```
toObject(): {[key: string]: V}

```

#### INHERITED FROM

```
Iterable#toObject
```

#### DISCUSSION

Throws if keys are not strings.

#### Conversion to Collections

### toMap()

Converts this Iterable to a Map, Throws if keys are not hashable.

```
toMap(): Map<number, T>

```

#### INHERITED FROM

```
Iterable#toMap
```

#### DISCUSSION

Note: This is equivalent to `Map(this.toKeyedSeq())`, but provided for convenience and to allow for chained expressions.

### toOrderedMap()

Converts this Iterable to a Map, maintaining the order of iteration.

```
toOrderedMap(): OrderedMap<number, T>

```

#### INHERITED FROM

```
Iterable#toOrderedMap
```

#### DISCUSSION

Note: This is equivalent to `OrderedMap(this.toKeyedSeq())`, but provided for convenience and to allow for chained expressions.

### toSet()

Converts this Iterable to a Set, discarding keys. Throws if values are not hashable.

```
toSet(): Set<T>

```

#### INHERITED FROM

```
Iterable#toSet
```

#### DISCUSSION

Note: This is equivalent to `Set(this)`, but provided to allow for chained expressions.

### toOrderedSet()

Converts this Iterable to a Set, maintaining the order of iteration and discarding keys.

```
toOrderedSet(): OrderedSet<T>

```

#### INHERITED FROM

```
Iterable#toOrderedSet
```

#### DISCUSSION

Note: This is equivalent to `OrderedSet(this.valueSeq())`, but provided for convenience and to allow for chained expressions.

### toList()

Converts this Iterable to a List, discarding keys.

```
toList(): List<T>

```

#### INHERITED FROM

```
Iterable#toList
```

#### DISCUSSION

Note: This is equivalent to `List(this)`, but provided to allow for chained expressions.

### toStack()

Converts this Iterable to a Stack, discarding keys. Throws if values are not hashable.

```
toStack(): Stack<T>

```

#### INHERITED FROM

```
Iterable#toStack
```

#### DISCUSSION

Note: This is equivalent to `Stack(this)`, but provided to allow for chained expressions.

#### Iterators

### keys()

An iterator of this `Iterable`'s keys.

```
keys(): Iterator<number>

```

#### INHERITED FROM

```
Iterable#keys
```

#### DISCUSSION

Note: this will return an ES6 iterator which does not support Immutable JS sequence algorithms. Use `keySeq` instead, if this is what you want.

### values()

An iterator of this `Iterable`'s values.

```
values(): Iterator<T>

```

#### INHERITED FROM

```
Iterable#values
```

#### DISCUSSION

Note: this will return an ES6 iterator which does not support Immutable JS sequence algorithms. Use `valueSeq` instead, if this is what you want.

### entries()

An iterator of this `Iterable`'s entries as `[key, value]` tuples.

```
entries(): Iterator<Array<any>>

```

#### INHERITED FROM

```
Iterable#entries
```

#### DISCUSSION

Note: this will return an ES6 iterator which does not support Immutable JS sequence algorithms. Use `entrySeq` instead, if this is what you want.

#### Iterables (Seq)

### keySeq()

Returns a new Seq.Indexed of the keys of this Iterable, discarding values.

```
keySeq(): Seq.Indexed<number>

```

#### INHERITED FROM

```
Iterable#keySeq
```

### valueSeq()

Returns an Seq.Indexed of the values of this Iterable, discarding keys.

```
valueSeq(): Seq.Indexed<T>

```

#### INHERITED FROM

```
Iterable#valueSeq
```

### entrySeq()

Returns a new Seq.Indexed of [key, value] tuples.

```
entrySeq(): Seq.Indexed<Array<any>>

```

#### INHERITED FROM

```
Iterable#entrySeq
```

#### Sequence algorithms

### map()

Returns a new Iterable of the same type with values passed through a `mapper` function.

```
map<M>(
mapper: (value?: T, key?: number, iter?: Iterable<number, T>) => M,
context?: any): Iterable<number, M>

```

#### INHERITED FROM

```
Iterable#map
```

#### EXAMPLE

`Seq({ a: 1, b: 2 }).map(x => 10 * x)// Seq { a: 10, b: 20 }`

### filter()

Returns a new Iterable of the same type with only the entries for which the `predicate`function returns true.

```
filter(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#filter
```

#### EXAMPLE

`Seq({a:1,b:2,c:3,d:4}).filter(x => x % 2 === 0)// Seq { b: 2, d: 4 }`

### filterNot()

Returns a new Iterable of the same type with only the entries for which the `predicate`function returns false.

```
filterNot(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#filterNot
```

#### EXAMPLE

`Seq({a:1,b:2,c:3,d:4}).filterNot(x => x % 2 === 0)// Seq { a: 1, c: 3 }`

### reverse()

Returns a new Iterable of the same type in reverse order.

```
reverse(): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#reverse
```

### sort()

Returns a new Iterable of the same type which includes the same entries, stably sorted by using a `comparator`.

```
sort(comparator?: (valueA: T, valueB: T) => number): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#sort
```

#### DISCUSSION

If a `comparator` is not provided, a default comparator uses `<` and `>`.

`comparator(valueA, valueB)`:

- Returns `0` if the elements should not be swapped.
- Returns `-1` (or any negative number) if `valueA` comes before `valueB`
- Returns `1` (or any positive number) if `valueA` comes after `valueB`
- Is pure, i.e. it must always return the same value for the same pair of values.

When sorting collections which have no defined order, their ordered equivalents will be returned. e.g. `map.sort()` returns OrderedMap.

### sortBy()

Like `sort`, but also accepts a `comparatorValueMapper` which allows for sorting by more sophisticated means:

```
sortBy<C>(
comparatorValueMapper: (
value?: T,
key?: number,
iter?: Iterable<number, T>) => C,
comparator?: (valueA: C, valueB: C) => number): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#sortBy
```

#### EXAMPLE

`hitters.sortBy(hitter => hitter.avgHits);`

### groupBy()

Returns a `Iterable.Keyed` of `Iterable.Keyeds`, grouped by the return value of the`grouper` function.

```
groupBy<G>(
grouper: (value?: T, key?: number, iter?: Iterable<number, T>) => G,
context?: any): Seq.Keyed<G, Iterable<number, T>>

```

#### INHERITED FROM

```
Iterable#groupBy
```

#### DISCUSSION

Note: This is always an eager operation.

#### Side effects

### forEach()

The `sideEffect` is executed for every entry in the Iterable.

```
forEach(
sideEffect: (value?: T, key?: number, iter?: Iterable<number, T>) => any,
context?: any): number

```

#### INHERITED FROM

```
Iterable#forEach
```

#### DISCUSSION

Unlike `Array#forEach`, if any call of `sideEffect` returns `false`, the iteration will stop. Returns the number of entries iterated (including the last iteration which returned false).

#### Creating subsets

### slice()

Returns a new Iterable of the same type representing a portion of this Iterable from start up to but not including end.

```
slice(begin?: number, end?: number): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#slice
```

#### DISCUSSION

If begin is negative, it is offset from the end of the Iterable. e.g. `slice(-2)` returns a Iterable of the last two entries. If it is not provided the new Iterable will begin at the beginning of this Iterable.

If end is negative, it is offset from the end of the Iterable. e.g. `slice(0, -1)` returns an Iterable of everything but the last entry. If it is not provided, the new Iterable will continue through the end of this Iterable.

If the requested slice is equivalent to the current Iterable, then it will return itself.

### rest()

Returns a new Iterable of the same type containing all entries except the first.

```
rest(): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#rest
```

### butLast()

Returns a new Iterable of the same type containing all entries except the last.

```
butLast(): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#butLast
```

### skip()

Returns a new Iterable of the same type which excludes the first `amount` entries from this Iterable.

```
skip(amount: number): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#skip
```

### skipLast()

Returns a new Iterable of the same type which excludes the last `amount` entries from this Iterable.

```
skipLast(amount: number): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#skipLast
```

### skipWhile()

Returns a new Iterable of the same type which includes entries starting from when`predicate` first returns false.

```
skipWhile(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#skipWhile
```

#### EXAMPLE

`Seq.of('dog','frog','cat','hat','god')  .skipWhile(x => x.match(/g/))// Seq [ 'cat', 'hat', 'god' ]`

### skipUntil()

Returns a new Iterable of the same type which includes entries starting from when`predicate` first returns true.

```
skipUntil(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#skipUntil
```

#### EXAMPLE

`Seq.of('dog','frog','cat','hat','god')  .skipUntil(x => x.match(/hat/))// Seq [ 'hat', 'god' ]`

### take()

Returns a new Iterable of the same type which includes the first `amount` entries from this Iterable.

```
take(amount: number): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#take
```

### takeLast()

Returns a new Iterable of the same type which includes the last `amount` entries from this Iterable.

```
takeLast(amount: number): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#takeLast
```

### takeWhile()

Returns a new Iterable of the same type which includes entries from this Iterable as long as the `predicate` returns true.

```
takeWhile(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#takeWhile
```

#### EXAMPLE

`Seq.of('dog','frog','cat','hat','god')  .takeWhile(x => x.match(/o/))// Seq [ 'dog', 'frog' ]`

### takeUntil()

Returns a new Iterable of the same type which includes entries from this Iterable as long as the `predicate` returns false.

```
takeUntil(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#takeUntil
```

#### EXAMPLE

`Seq.of('dog','frog','cat','hat','god').takeUntil(x => x.match(/at/))// ['dog', 'frog']`

#### Combination

### concat()

Returns a new Iterable of the same type with other values and iterable-like concatenated to this one.

```
concat(...valuesOrIterables: any[]): Iterable<number, T>

```

#### INHERITED FROM

```
Iterable#concat
```

#### DISCUSSION

For Seqs, all entries will be present in the resulting iterable, even if they have the same key.

### flatten()

Flattens nested Iterables.

```
flatten(depth?: number): Iterable<any, any>
flatten(shallow?: boolean): Iterable<any, any>

```

#### INHERITED FROM

```
Iterable#flatten
```

#### DISCUSSION

Will deeply flatten the Iterable by default, returning an Iterable of the same type, but a`depth` can be provided in the form of a number or boolean (where true means to shallowly flatten one level). A depth of 0 (or shallow: false) will deeply flatten.

Flattens only others Iterable, not Arrays or Objects.

Note: `flatten(true)` operates on Iterable> and returns Iterable

### flatMap()

Flat-maps the Iterable, returning an Iterable of the same type.

```
flatMap<MK, MV>(
mapper: (
value?: T,
key?: number,
iter?: Iterable<number, T>) => Iterable<MK, MV>,
context?: any): Iterable<MK, MV>
flatMap<MK, MV>(
mapper: (value?: T, key?: number, iter?: Iterable<number, T>) => any,
context?: any): Iterable<MK, MV>

```

#### INHERITED FROM

```
Iterable#flatMap
```

#### DISCUSSION

Similar to `iter.map(...).flatten(true)`.

### interpose()

Returns an Iterable of the same type with `separator` between each item in this Iterable.

```
interpose(separator: T): Iterable.Indexed<T>

```

#### INHERITED FROM

```
Iterable.Indexed#interpose
```

### interleave()

Returns an Iterable of the same type with the provided `iterables` interleaved into this iterable.

```
interleave(...iterables: Array<Iterable<any, T>>): Iterable.Indexed<T>

```

#### INHERITED FROM

```
Iterable.Indexed#interleave
```

#### DISCUSSION

The resulting Iterable includes the first item from each, then the second from each, etc.

```
I.Seq.of(1,2,3).interleave(I.Seq.of('A','B','C'))
// Seq [ 1, 'A', 2, 'B', 3, 'C' ]
```

The shortest Iterable stops interleave.

```
I.Seq.of(1,2,3).interleave(
  I.Seq.of('A','B'),
  I.Seq.of('X','Y','Z')
)
// Seq [ 1, 'A', 'X', 2, 'B', 'Y' ]
```

### splice()

Splice returns a new indexed Iterable by replacing a region of this Iterable with new values. If values are not provided, it only skips the region to be removed.

```
splice(index: number, removeNum: number, ...values: any[]): Iterable.Indexed<T>

```

#### INHERITED FROM

```
Iterable.Indexed#splice
```

#### DISCUSSION

`index` may be a negative number, which indexes back from the end of the Iterable.`s.splice(-2)` splices after the second to last item.

```
Seq(['a','b','c','d']).splice(1, 2, 'q', 'r', 's')
// Seq ['a', 'q', 'r', 's', 'd']
```

### zip()

Returns an Iterable of the same type "zipped" with the provided iterables.

```
zip(...iterables: Array<Iterable<any, any>>): Iterable.Indexed<any>

```

#### INHERITED FROM

```
Iterable.Indexed#zip
```

#### DISCUSSION

Like `zipWith`, but using the default `zipper`: creating an `Array`.

```
var a = Seq.of(1, 2, 3);
var b = Seq.of(4, 5, 6);
var c = a.zip(b); // Seq [ [ 1, 4 ], [ 2, 5 ], [ 3, 6 ] ]
```

### zipWith()

Returns an Iterable of the same type "zipped" with the provided iterables by using a custom `zipper` function.

```
zipWith<U, Z>(
zipper: (value: T, otherValue: U) => Z,
otherIterable: Iterable<any, U>): Iterable.Indexed<Z>
zipWith<U, V, Z>(
zipper: (value: T, otherValue: U, thirdValue: V) => Z,
otherIterable: Iterable<any, U>,
thirdIterable: Iterable<any, V>): Iterable.Indexed<Z>
zipWith<Z>(
zipper: (...any: Array<any>) => Z,
...iterables: Array<Iterable<any, any>>): Iterable.Indexed<Z>

```

#### INHERITED FROM

```
Iterable.Indexed#zipWith
```

#### EXAMPLE

`var a = Seq.of(1, 2, 3);var b = Seq.of(4, 5, 6);var c = a.zipWith((a, b) => a + b, b); // Seq [ 5, 7, 9 ]`

#### Reducing a value

### reduce()

Reduces the Iterable to a value by calling the `reducer` for every entry in the Iterable and passing along the reduced value.

```
reduce<R>(
reducer: (
reduction?: R,
value?: T,
key?: number,
iter?: Iterable<number, T>) => R,
initialReduction?: R,
context?: any): R

```

#### INHERITED FROM

```
Iterable#reduce
```

#### SEE

`Array#reduce`.

#### DISCUSSION

If `initialReduction` is not provided, or is null, the first item in the Iterable will be used.

### reduceRight()

Reduces the Iterable in reverse (from the right side).

```
reduceRight<R>(
reducer: (
reduction?: R,
value?: T,
key?: number,
iter?: Iterable<number, T>) => R,
initialReduction?: R,
context?: any): R

```

#### INHERITED FROM

```
Iterable#reduceRight
```

#### DISCUSSION

Note: Similar to this.reverse().reduce(), and provided for parity with`Array#reduceRight`.

### every()

True if `predicate` returns true for all entries in the Iterable.

```
every(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any): boolean

```

#### INHERITED FROM

```
Iterable#every
```

### some()

True if `predicate` returns true for any entry in the Iterable.

```
some(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any): boolean

```

#### INHERITED FROM

```
Iterable#some
```

### join()

Joins values together as a string, inserting a separator between each. The default separator is `","`.

```
join(separator?: string): string

```

#### INHERITED FROM

```
Iterable#join
```

### isEmpty()

Returns true if this Iterable includes no values.

```
isEmpty(): boolean

```

#### INHERITED FROM

```
Iterable#isEmpty
```

#### DISCUSSION

For some lazy `Seq`, `isEmpty` might need to iterate to determine emptiness. At most one iteration will occur.

### count()

Returns the size of this Iterable.

```
count(): number
count(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any): number

```

#### INHERITED FROM

```
Iterable#count
```

#### DISCUSSION

Regardless of if this Iterable can describe its size lazily (some Seqs cannot), this method will always return the correct size. E.g. it evaluates a lazy `Seq` if necessary.

If `predicate` is provided, then this returns the count of entries in the Iterable for which the `predicate` returns true.

### countBy()

Returns a `Seq.Keyed` of counts, grouped by the return value of the `grouper` function.

```
countBy<G>(
grouper: (value?: T, key?: number, iter?: Iterable<number, T>) => G,
context?: any): Map<G, number>

```

#### INHERITED FROM

```
Iterable#countBy
```

#### DISCUSSION

Note: This is not a lazy operation.

#### Search for value

### find()

Returns the first value for which the `predicate` returns true.

```
find(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any,
notSetValue?: T): T

```

#### INHERITED FROM

```
Iterable#find
```

### findLast()

Returns the last value for which the `predicate` returns true.

```
findLast(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any,
notSetValue?: T): T

```

#### INHERITED FROM

```
Iterable#findLast
```

#### DISCUSSION

Note: `predicate` will be called for each entry in reverse.

### findEntry()

Returns the first [key, value] entry for which the `predicate` returns true.

```
findEntry(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any,
notSetValue?: T): Array<any>

```

#### INHERITED FROM

```
Iterable#findEntry
```

### findLastEntry()

Returns the last [key, value] entry for which the `predicate` returns true.

```
findLastEntry(
predicate: (value?: T, key?: number, iter?: Iterable<number, T>) => boolean,
context?: any,
notSetValue?: T): Array<any>

```

#### INHERITED FROM

```
Iterable#findLastEntry
```

#### DISCUSSION

Note: `predicate` will be called for each entry in reverse.

### findKey()

Returns the key for which the `predicate` returns true.

```
findKey(
predicate: (
value?: T,
key?: number,
iter?: Iterable.Keyed<number, T>) => boolean,
context?: any): number

```

#### INHERITED FROM

```
Iterable#findKey
```

### findLastKey()

Returns the last key for which the `predicate` returns true.

```
findLastKey(
predicate: (
value?: T,
key?: number,
iter?: Iterable.Keyed<number, T>) => boolean,
context?: any): number

```

#### INHERITED FROM

```
Iterable#findLastKey
```

#### DISCUSSION

Note: `predicate` will be called for each entry in reverse.

### keyOf()

Returns the key associated with the search value, or undefined.

```
keyOf(searchValue: T): number

```

#### INHERITED FROM

```
Iterable#keyOf
```

### lastKeyOf()

Returns the last key associated with the search value, or undefined.

```
lastKeyOf(searchValue: T): number

```

#### INHERITED FROM

```
Iterable#lastKeyOf
```

### max()

Returns the maximum value in this collection. If any values are comparatively equivalent, the first one found will be returned.

```
max(comparator?: (valueA: T, valueB: T) => number): T

```

#### INHERITED FROM

```
Iterable#max
```

#### DISCUSSION

The `comparator` is used in the same way as `Iterable#sort`. If it is not provided, the default comparator is `>`.

When two values are considered equivalent, the first encountered will be returned. Otherwise, `max` will operate independent of the order of input as long as the comparator is commutative. The default comparator `>` is commutative *only* when types do not differ.

If `comparator` returns 0 and either value is NaN, undefined, or null, that value will be returned.

### maxBy()

Like `max`, but also accepts a `comparatorValueMapper` which allows for comparing by more sophisticated means:

```
maxBy<C>(
comparatorValueMapper: (
value?: T,
key?: number,
iter?: Iterable<number, T>) => C,
comparator?: (valueA: C, valueB: C) => number): T

```

#### INHERITED FROM

```
Iterable#maxBy
```

#### EXAMPLE

`hitters.maxBy(hitter => hitter.avgHits);`

### min()

Returns the minimum value in this collection. If any values are comparatively equivalent, the first one found will be returned.

```
min(comparator?: (valueA: T, valueB: T) => number): T

```

#### INHERITED FROM

```
Iterable#min
```

#### DISCUSSION

The `comparator` is used in the same way as `Iterable#sort`. If it is not provided, the default comparator is `<`.

When two values are considered equivalent, the first encountered will be returned. Otherwise, `min` will operate independent of the order of input as long as the comparator is commutative. The default comparator `<` is commutative *only* when types do not differ.

If `comparator` returns 0 and either value is NaN, undefined, or null, that value will be returned.

### minBy()

Like `min`, but also accepts a `comparatorValueMapper` which allows for comparing by more sophisticated means:

```
minBy<C>(
comparatorValueMapper: (
value?: T,
key?: number,
iter?: Iterable<number, T>) => C,
comparator?: (valueA: C, valueB: C) => number): T

```

#### INHERITED FROM

```
Iterable#minBy
```

#### EXAMPLE

`hitters.minBy(hitter => hitter.avgHits);`

### indexOf()

Returns the first index at which a given value can be found in the Iterable, or -1 if it is not present.

```
indexOf(searchValue: T): number

```

#### INHERITED FROM

```
Iterable.Indexed#indexOf
```

### lastIndexOf()

Returns the last index at which a given value can be found in the Iterable, or -1 if it is not present.

```
lastIndexOf(searchValue: T): number

```

#### INHERITED FROM

```
Iterable.Indexed#lastIndexOf
```

### findIndex()

Returns the first index in the Iterable where a value satisfies the provided predicate function. Otherwise -1 is returned.

```
findIndex(
predicate: (value?: T, index?: number, iter?: Iterable.Indexed<T>) => boolean,
context?: any): number

```

#### INHERITED FROM

```
Iterable.Indexed#findIndex
```

### findLastIndex()

Returns the last index in the Iterable where a value satisfies the provided predicate function. Otherwise -1 is returned.

```
findLastIndex(
predicate: (value?: T, index?: number, iter?: Iterable.Indexed<T>) => boolean,
context?: any): number

```

#### INHERITED FROM

```
Iterable.Indexed#findLastIndex
```

#### Comparison

### isSubset()

True if `iter` includes every value in this Iterable.

```
isSubset(iter: Iterable<any, T>): boolean
isSubset(iter: Array<T>): boolean

```

#### INHERITED FROM

```
Iterable#isSubset
```

### isSuperset()

True if this Iterable includes every value in `iter`.

```
isSuperset(iter: Iterable<any, T>): boolean
isSuperset(iter: Array<T>): boolean

```

#### INHERITED FROM

```
Iterable#isSuperset
```

This documentation is generated from [Immutable.d.ts](https://github.com/facebook/immutable-js/blob/master/type-definitions/Immutable.d.ts). Pull requests and [Issues](https://github.com/facebook/immutable-js/issues) welcome.
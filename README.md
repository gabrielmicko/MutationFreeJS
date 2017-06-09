## Describing how to manipulate object or array in an immutable way 

### What is immutability?
All updates return new values, but internally structures are shared to drastically reduce memory usage (and GC thrashing). This means that if you append to a vector with 1000 elements, it does not actually create a new vector 1001-elements long. Most likely, internally only a few small objects are allocated.

ref: [Using immutable data structures](http://jlongster.com/Using-Immutable-Data-Structures-in-JavaScript#Immutable.js)

##### Adding one element to an Array
  ```js
const addElementToAnArray = (list, element) => {
	return [...list, element];
}

addElementToAnArray([1, 2, 3], 4);
//[1,2,3,4] 
```

##### Remove item from an Array according to an index
  ```js
const removeItemFromAnArray = (list, index) => {
	return [
		...list.slice(0, index),
		...list.slice(index + 1)
	]
}

removeItemFromAnArray([1, 2, 3], 1)
//[1,3]
```

##### Increment an item in an Array containing numbers
 ```js
const incrementAnItemInAnArray = (list, index) => {
	return [
		...list.slice(0, index),
		list[index] + 1,
		...list.slice(index + 1)
	]
}

incrementAnItemInAnArray([1, 2, 3], 1)
//[1,3,3]
```

##### Replace an item in an array 
  ```js
const replaceAnItemInAnArray = (list, index, newItem) => {
	return [
		...list.slice(0, index),
		newItem,
		...list.slice(index + 1)
	]
}

replaceAnItemInAnArray([1, 3, 3], 1, 2)
//[1,2,3] 
```

##### Change a boolean in an object
 ```js
const changeBooleanInAnObject = (item) => {
	return Object.assign({}, item, {
		isActive: !item.isActive
	})
}

changeBooleanInAnObject({isActive: false})
//{"isActive":true} 
```

##### Change a boolean in an object (with Babel Stage 2 preset)
 ```js
const changeBooleanInAnObject = (item) => {
	return {
		...item,
		isActive: !item.isActive
	}
}

changeBooleanInAnObject({isActive: false})
//{"isActive":true} 
```

#####  Toggle every isActive property in an array of objects
 ```js
const toggleAllIsActiveProperty = (list) => {
	return list.map(item => {
		return {
			...item,
			isActive: !item.isActive
		}
	});
}

toggleAllIsActiveProperty([{isActive: false}, {isActive: false}, {isActive: false}])
//[{"isActive":true},{"isActive":true},{"isActive":true}]
```

Comments or issues are welcome
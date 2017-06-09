## Describing how to manipulate object or array in an immmutable way 

##### Adding one element to an Array
  ```js
(list, element) => {
	return [...list, element];
}
```

##### Remove item from an Array according to an index
  ```js
(list, index) => {
	return [
		...list.slice(0, index),
		...list.slice(index + 1)
	]
}
```

##### Increment an item in an Array containing numbers
 ```js
(list, index) => {
	return [
		...list.slice(0, index),
		list[index] + 1,
		...list.slice(index + 1)
	]
}
```

##### Replace an item in an array 
  ```js
(list, index, newItem) => {
	return [
		...list.slice(0, index),
		newItem,
		...list.slice(index + 1)
	]
}
```

##### Change a boolean in an object
 ```js
(item) => {
	return Object.assign({}, item, {
		isActive: !item.isActive
	})
}
```

##### Change a boolean in an object (with Babel Stage 2 preset)
 ```js
(item) => {
	return {
		...item,
		isActive: !item.isActive
	}
}
```
#####  Toggle every isActive property in an array of objects
 ```js
(list) => {
	return list.map(item => {
		return {
			...item,
			isActive: !item.isActive
		}
	});
}
```
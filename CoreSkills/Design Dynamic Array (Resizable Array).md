
Design a [Dynamic Array](https://neetcode.io/courses/dsa-for-beginners/3) (aka a resizable array) class, such as an `ArrayList` in Java or a `vector` in C++.

[Documentation for design dynamic array](https://www.geeksforgeeks.org/dsa/how-do-dynamic-arrays-work/)

Your `DynamicArray` class should support the following operations:

- `DynamicArray(int capacity)` will initialize an empty array with a capacity of `capacity`, where `capacity > 0`.
```javascript
constructor(capacity) {
  this.capacity = capacity; // This initiates a variable for keeping track of the capacity of the

  this.size = 0; // This is used to track the size of the elements in the array
  
  if (capacity > 0) { // // Check that the capacity of the array is greater than 0
  
	this.array = new Array(capacity); // // Initiates the new array with capacity length
	}
}
```

- `int get(int i)` will return the element at index `i`. Assume that index `i` is valid.
```javascript
get(i) {
  return this.array[i]; // Returns the element at index i
}
```

- `void set(int i, int n)` will set the element at index `i` to `n`. Assume that index `i` is valid.
```javascript 
set(i, n) {
  this.array[i] = n;
}
```

- `void pushback(int n)` will push the element `n` to the end of the array.
```javascript 
pushback(n) {
  if (this.size === this.capacity) {
    this.resize(this.array.length + 1)
  }
  this.array[this.size] = n
  this.size = this.size + 1
}
```

- `int popback()` will pop and return the element at the end of the array. Assume that the array is non-empty.
```javascript
popback() {
        if (this.array.length > 0){
            this.size = this.size - 1;
            return this.array[this.size];
        }
    }
```

- `void resize()` will _double_ the capacity of the array.
```javascript
resize() {
  this.capacity = this.capacity * 2;
  
  let newArray = new Array(this.capacity);
  
  for (let i = 0; i < this.size; i++) {
    newArray[i] = this.array[i];
  }
  
  this.array = newArray;
}
```

- `int getSize()` will return the number of elements in the array.
```javascript
getSize() {
  return this.size;
}
```

- `int getCapacity()` will return the capacity of the array.
```javascript
getCapacity() {
  return this.capacity;
}
```


If we call `void pushback(int n)` but the array is full, we should resize the array first.
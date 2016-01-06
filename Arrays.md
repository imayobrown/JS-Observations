#Array
---

Arrays are really just a type of object that is optimized to bind values to successive numeric integer keys. It has built in property functions that perform operations/actions on its elements. These operations do not perform in place modification of the array (the elements in the array are never changed) but rather they return a new array or object with the desired changes affected to its elements.

## Array Functions

####push

	array.push( item );

Adds an element **item** to the end of the array. Does not return any value.

####pop

	array.pop()

Removes an element from the end of the array and returns it.

####forEach

	array.forEach( action )

Applies an **action** to each element of the array. The action is a function that is passed every element of the array one argument at a time by the forEach method. **action** is of the form:

	function( item ) {
		...
	}

####filter

	array.filter( predicate )

Applies **predicate** to each element of the array and returns an array populated by only the elements that return true when passed as arguments to the predicate. **predicate** takes only a single argument, returns a boolean value and is of the form: 

	function( item ) {
		...
		return boolean;
	}

####map

	 array.map( action )

Maps each element of the array to a new element based on the **action** passed. Returns a new array with each of the elements in the original array mapped according to **action**. The return value of the **action** function is the item that will be added to the array returned by **map**. The returned mapped array and the original array will have the same length. **action** is of the form:

	function( item ) {
		...
		return newItem;
	}


####reduce

	array.reduce( operation )

Reduces an array to a single value by using **operation**. The **operation** is called once for every element of the array. **operation** is of the form:

	function( lastReturnValue, currentArrayValue ) {
		...
		return newReturnValue;
	}

Two arguments are passed to **operation**. The first argument *lastReturnValue* is the value that was returned from the last run of **operation** and the second argument *currentArrayValue* is the next value of the array being passed to **operation**. Reduce is very useful for things like summing all of the values of an array or combining them into a aggregate value.
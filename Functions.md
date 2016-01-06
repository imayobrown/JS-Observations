#Functions
---

##Function Methods

Since functions in JavaScript are technically objects they can have methods. Here are some of the common methods used with functions.

####apply

	function.apply( null, arg)

Used to call a function with an array listing their arguments. **arg** is an array with all of the arguments that are to be enumerated in the call to function. For example:

	arg = [ 1, 2, 3, 4, 5 ];
	calledFunction.apply( null, arg );

Will result in a function call that looks like:

	calledFunction( 1, 2, 3, 4, 5 );

####bind

	calledFunction.bind( null, arg )

This line returns a function that calls **calledFunction** with **arg** as the first argument followed by any additional arguments passed to the bound function. Generally **arg** is a constant argument, the same value is passed as the first argument every time the new bound function is called.
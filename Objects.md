#Objects
---

##Static Objects/Object Literals
Static objects (object literals) can be created in javascript. These objects are much like dictionaries or hash maps in other languages. Technically every javascript object is a hash map/dictionary. Each key in the dictionary is an "attribute" which can be either just a data member or a function. In javascript object functions are just attributes that are mapped to functions instead of static data objects. Here is an example of the code used to create a static object (one that has not constructor or prototype):

    var object = {property1: "This property is a string",
				  property2: 2, //This property is a numeric
				  property3: function(){return "This is a fucntion";}  //This property is actually a function
				 };
	
	console.log(object.property1); //Returns: This property is a string
	console.log(object.property2); //Returns: 2
	console.log(object.property3()); //Returns: "This is a function"

This object will only ever exist as the variable object within the namespace that it is defined. No objects can be derived from it and it can't be used for any prototype functionality. However, it can be added to dynamically later in the code to extend it. For example:

	object.newProperty = "New property";
	console.log(newProperty); //Will output "New property" to the console.


##Object Creation using Constructor

Objects can be created in more classical fashion using constructor functions. This manner will allow the object definition to have a prototype attribute that can be used to dynamically add and modify the class. When created in this manner the entire definition and structure of the class are contained in the constructor function definition. Here is an example of how a object definition can be constructed:

	var Person = function Person(name, age) {
		this.name = name;
		this.age = age;
		this.getAge = function() {
			return this.age;
		};
	};

Here we define a Person object with two properties/attributes, name and age, and a single getter method getAge(). Just like above we can see that the methods on this object are actually variables that have been assigned a function object. Therefore we must have a semicolon after the function definition because in actuality it is part of the expression assigning the anonymous function definition to the object member getAge. 

####Prototypes

As previously stated, since this object was defined using a constructor it now has a prototype property. This property is assigned at runtime by the interpreter once it recognizes that this object was defined with a constructor rather than as an object literal. **The prototype property is essentially a pointer to the constructor function. By accessing it we can dynamically modify the object definition.** Modifications to an object using the prototype property will propagate to any objects created from Person (using new Person()) or any objects that have inherited from Person. Only objects created using a constructor will be assigned this property, object literals do not have this and therefore the object instance must be modified directly. This is the power of the prototype property, it allows changes to an object definition to be made in one place and have those changes reflected in numerous other objects simultaneously. Where as if objects are always created using object literals then each object has to be modified manually even if they share a common structure. Here is an example of accessing and utilizing the prototype property of the Person class defined above: 
	
	//Create a Person object named John
	var John = new Person('John','25');

	console.log(John.getName()); //Error: getName undefined for John. 
	
	Person.prototype.getName = function() {
		return this.name;
	};

	console.log(John.getName()); //Prints "John" to console

Here we can see that even though we didnt make any changes to John he was updated with the change we made to Person using its prototype property. This illustrates the propagation of the changes to Person to all of the object instances created from its definition.

The distinction between the way an object has a prototype (retrieved by *Object.getPrototypeOf* ) and the way a prototype is associated with a constructor is described very clearly in "Eloquent JavaScript" by Martin Haverbeke in Chapter 6, section header "Prototypes":

>It is important to note the distinction between the way a prototype is associated with a constructor (through its prototype property) and the way objects have a prototype (which can be retrieved with Object.getPrototypeOf). The actual prototype of a constructor is Function.prototype since constructors are functions. Its prototype property will be the prototype of instances created through it but is not its own prototype.

From his explanation we see that prototypes are passed by association with constructors and the *prototype* property of an object may not match its actual prototype because the *prototype* property is the value tied to the objects constructor. For example continuing using the example from above:

	//Override the Object.toString method for the Person class in order to print an 
	//informative value when queried. Otherwise it will simply print the default value for an
	//object which is '{}'
	Person.prototype.toString = function() { return 'Person'; }

	console.log(Object.getPrototypeOf(Person.prototype).toString());
	// function Empty()  {}

	console.log(Person.prototype);
	// {}

	console.log(Object.getPrototypeOf(John).toString());
	// Person

	console.log(John.prototype);
	// undefined
	
Here we can see that John, since it is an object created from a constructor has no **property** *prototype* but he does actually have a prototype which is 'Person'. With the Person we can see that it is a constructor therefore it has a *prototype* **property** which is different from its actual prototype. Its actual prototype is function Empty().


##Object Methods

####Object.defineProperty

	Object.defineProperty( obj, propertyKey, options )

Used to define a property on an object with a list of options to determine the characteristics of the property. Very useful when defining properties on prototypes to keep them from being enumerable or controlling other aspects of their behavior. Example adding property *key* with value *static* to a prototype:

	Object.defineProperty( Person.prototype, 'key', {
		enumerable: false,
		configurable: false,
		writable: false,
		value: 'static'
	});
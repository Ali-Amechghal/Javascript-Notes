# Speaking JS  (Part 1)

	List of notes and tricks exctracted from SpeakingJS Book , greate Boook by the way :)
	This part cover Definitions ,  Primitives , Objects , Null vs Undefiend , truty and falsy values
	
## Ecmascript 
	
	Officiel name of javascript , used to refer to the specifications

## Javascript Influence
	
	Javascript is influenced by many programming languages :
		- Java for the synthaxe part
		- Schema and Awk for the first class functions
		- Self for the prototypal inheritance
		- Perl / Python for the strings a, arrays , regex 

## Note 1 : Javascript vs other languages
	
	In other languges your learn the language fezatures but in javascript you should learn the pattern,
	Patterns that will allows bypass unavailable functions.

## Note 2 : Statement Vs Expression

	Statement  do things while Expression produce value

	Expression  :
			```javascript
				var result = (y>=0) ? y: X;
			```

	Statement  :
			```javascript
				if(y>=0)
					result = y;
				else
					result = x;

			```

## Primitives

	Primitives types : boolean, string, null undefined, number
	Primitives are immutable , they cannot be changed

	```javascript
		'str'.length = 2; //no effect
		'str'.newProp = 1 //no effect we cannot add the property to primitives 'str'.newProp call it will return 'undefined'
	```

	Primive dont have itw own methods but it referes to the wrapper methods
	'abc'.chatAt === String.prototype.charAt // return true , its the same

	NB : Unkonw propoerty return always 'undefiend'
### Coercion
	implictit type conversion , '1' * '2' -> 2
	Coercion support Number , String , Boolean , Object
### Wrappers
	Convert primitive to wrapper object:
	```javascript
		var str = new String('str primitive value');
		typeof str // 'object'
		'abc' instanceof String // false , a primitive value is not an object of its wrapper
		str instanceof String // true 
	```
	unwrapper the object to primitive value
	```javascript
	    var numInstance = new Number('123');
		Number(numInstance) // 123
		var num = Number(numInstance)
		//or
		var num  = numInstance.ValueOf();
		typeof num // 'number'
	```
	Unwrappers works for Number, Object and String but not boolean
	Object() can convert to any type , typeof (Object('str')) 'object' , and (Object('str') instanceof String return true)
	Object(undefined) return {}

	Number() :
			when we call Number() it will cal first valueOf() method if its not defined it will call toString()
			Numner({}) or Number(undefined)  return NaN
	

		


## Objects 
	
	Except the primiives all others things are obeject , Array , {} , Function , RegEx
	and We can add new property to object or change existing ones

## Undefined vs Null

	Undefined is equivalent to no value or unintialized variable , or missing parametre or inexistent object property
	
	```javascript
		var  a; 
		console.log(a); //undefined , unintialized variable
		function test(param){
			console.log(param);// undefined , missing parameter call
			console.log(typeof param) //undefined
		}
		test();//call without parameter

		//inexistent property
		var obj = {firstname:'Ali'}
		console.log(obj.lastname); //undefined
	```

	Null  is equivalent to no object exist , and you can use null as a value for initialization

	Undefiend and Null dont have any properties , and they are a falsy value 
	```javascript
		if(null) console.log('null true');
		 else console.log('null false'); //display null false

		if(undefined) console.log('undefined true');
		 else console.log('undefined false') ; // display undefined false
	 
	```
	You can shortcut the test of null and undefined by testing  it as falsy  value
	
	```javascript
		if(myvar === null ||  myvar === undefined )
		//same as		
		if(!myvar)
	```	

	Another difference between null and undefined is the type, null is considered as an object 

	```javascript
		typeof null // 'object'
		typeof undefined // ''undefined
	```

## Falsy values

	Empty string , O value , null , NaN ,  undefiend

## Truty values

	{} empty object is considered true
	[] empry array is considered true

## Binary logical

	&& return first if is false and second if the first is true
	|| return the first if is true and second if the result id false

	NaN && 'abc'  will return NaN
	123 && 'abc'  will return 'abc'

	'abc' || 123  will return abc
	 ''   || 123  will return 123



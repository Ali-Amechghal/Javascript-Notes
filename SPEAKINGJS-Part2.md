# Speaking JS  (Part 2)

	List of notes and tricks exctracted from SpeakingJS Book , greate Boook by the way :)
	This part cover Numbers, Strings  , Closure, Exception , and Arrays

## Numbers

	All numbers including float one are of type number , there no float , int 
	and All numberes are 64bits Floating point (double in java) , but Javascript hide ',' if there is not numbers after it

	Numebr()  : consider this constructor as kind of wrapper object in java , if it cannot convert the given value to Number , it will return NaN
	```javascript
		Number('abc') will return NaN
		Number('123') will return 123
		Number(new Number(123)) will return 123
		Number (new Number('123')) will return 123
		Number(null) will return 0 as Number(new Number(null)) too
		5  + null = 5 //null become 0
		undefiend == NaN //true
		null == 0 //true
		false == 0 ;  true == 1 //true
	```
	Invocking methods in literal number
	```javascript
		1..toString();
		1 .toString();
		(1).toString(); //my prefered one
		1.0 .toString(); //with floating point number
	``
	To parse a number from string or others objects always use Number() instead of parseFloat() , that will avoid some issues like :
		```javascript
 			//parseFloat() vs Number()
 			parseFloat(true) // NaN
 			Number(true) //1
		```
	To test if number is NaN , use one of this methods:
		```javascript
			isNaN(num) 
			value != value //compare a value with it self (NaN not equals to NaN)
		```	
	To generate Infinity "Constant" 
		```javascript
			1/-0  == -Infinity
			1/0  == Infinity
		```
## Strings
	Strings in javascript like in java are immutable , and 16bits unicode UTF-16, 4 hexa digits or 2 bytes

	var str = 'abc'
	you can access char in the using index , 
	str[1]  : 'b'
	you can use slice with string , slice is a method to extract a part of an array or string in our case
	```javascript
		str.slice(1) extract part of string straring from a given position until the end of string , it will print 'bc'
		str.slice(1,2) ; extract part of string from given position and until the end position , 'b'
		str.trim() // trim spaces 
		str.upperCase()
		str.lowerCase()
		str.indexOf('b') : get index of given char , it will print -1 if no 
		occurance found
		'str'.split('delimiter',[limit]) //split a given string with , limit starting from 1st position
		'str'.replace(regex ,value);
		'str'.search(reg) //return first position
	```

	Escaping lines in String with \:
		```javascript
			var str = 'written \
						new Line';
		```
	Construct string from char code array:
		```javascript
			String.prototype.fromCharCode.apply(null , arr);
			String.prototype.charCodeAt(position);
		``
### Comparing two chars
	when you compare characters always unifiy the case or use localCompare() method
		```javascript
		    //test without unifying case
			'a' < 'b' //true
			'a' < 'B' //false
			//
		```


## Exceptions

	the catch in excpetion you should surround your code with the try/catch block 

	```javascript

		try{

			..code
		}catch(exception){
			//catch exception or throw it again 
			throw new Error(exception);
		}

	```	



## Closure

	when we return a function inside another function , we are creating a closure  , the returened function is connected to the variables of the functio that surrond it



	```javascript
		function increment (x){
 			return function(){
 				x++;
 				return x;

 			}

		}

		//use

		var next = increment(1);
		console.log(next()) //2;
		console.log(next()) //3;

	```	

	as we see the cloure is veru usefull but it can be dangerous in same case, you should use it carefully , let see what will happen with this example


	```javascript
	  var results = [];
	  for(i = 0 ; i < 5 ; i ++){
	  	return results.push(function(){
	  			return i;
	  		});
	  }
	  result[1]() // calling the first function in the array that normaly should return the result for the first element 0
	  			//but suprisly not , it will return the last value of i ; i  = 5;

	```
	to bypass this problem you should use IIFE (immediatly innoveked function expression), that will isolite the scope of current 'i'

	```javascript
	  var results = [];
	  for(i = 0 ; i < 5 ; i ++){
	  	(function(){
	  		var tmpI =  i;
	  		results.push(function(){
	  			return tmpI;
	  			});

	  	})();
	  	
	  }

	 ```

## Arrays

	some important array property and methods

	```javascript

		var arr = ['a' , 'b' ,'c '];
		arr.length
		arr[arr.length]  = 'd' //put 'd' in the last position+1 /: same as arr.push('d');
		arr.length = 2 //['a' , 'b' ] , since array is an object we can change its properties
		var 1 in arr // get true , cause there is an element in the second position

		//methods
		arr.slice(1,2) // return 'b'
		arr.slice(1) // return sb array with elements starting from 1 indice until the end
		arr.push('F') // put element in the end of array
		arr.pop() //return the last element and delete it from the array
		arr.shift() //remove the first element
		arr.unshift('X') //add element in the first position
		arr.reverse()
		arr.sort()
		arr.sort(comp) //function comp(a,b){return a - b};
		arr.splice(0,1,'A','B'); // delete 1 element from 0 and insert A,B 
		arr.splice(0,0,'A','B') // insert A, B in the position 0 without removing any element


	```


## Synthaxe
	some tips and tricks when about javascript synthaxe 
	always yse '()' when you want to use literal object inside eval method
		```javascript
			eval('{name:"name value"}') // it will consider object as string with "name value" as value
			//instead use ()
			eval('({name:"name value"})') // => {name:'name value'}
		```
		
	### ASI (Automatic Simicolon  Insertion)
			Javasctipt compiler insert automaticly the simicolon in this cases:
				- after a line terminator
				- afiter closing braces
				- end of file
			but not after return or after [] , or even after () , so consider  using simicolon as its a best practice;
	### Simicolon problems
		in some cases if you dont use ";" your code can break

		Ex 1 : 
			```javascript
				//what you type
				function test(){
					return 
					{
						name:'name value'
					}
				}
				//what you get
				function test(){
					return;
					{
						name:"name value";
					}
				}

			```	
		the compiler add ; in the end of line , so the function will return undefined and not the object as expected

		Ex 1 :
			The javascript compiler dont put simicolon after '()'
			```javascript
			   //what you type 
				function test(){}
				test()
				['a','b'].forEach(function (item){console.log(item)});
				//what you get
				test()
				undefined['a','b'].forEach(function (item){console.log(item)});
				//TypeError: Cannot read property 'b' of undefined

			```
## Operators
		the "+" operator can be used with arrays
		[1,2] + [3] : '1,23' :  it will convert arrays to strings and concatenate them

		void O // will return undefined , usefull when you want to be sure you test about undefined
		void window.open('url') //if you dont want to repalce current document object
		
### Comparing 
		'abc' == new String('abc') //will return true
		'abc' === new String('abc') //will return false










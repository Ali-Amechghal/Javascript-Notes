# Speaking JS  (Part 2)

	List of notes and tricks exctracted from SpeakingJS Book , greate Boook by the way :)
	This part cover Numbers, Strings , Functions , Closure, Exception , and Arrays

## Numbers

	All numbers including float one are of type number , there no float , int 

	Numebr()  : consider this constructor as kind of wrapper object in java , if ti t cannot convert the given value to Number , it will return NaN
	```javascript
		Number('abc') will return NaN
		Number('123') will return 123
		Number(new Number(123)) will return 123
		Number (new Number('123')) will return 123
		Number(null) will return 0 as Number(new Number(null)) too

	```
## Strings

	
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
		str.indexOf('b') : get index of given char , it will print -1 if no occurance found
	```


## Functions
	
	One of the most important concept when you learn functions in javascript is the hoising , all functions are hoisted
	thats mean the function declation is moved to the top of the scope, consider this example


	```javascript
		function hoiz(){
			do(); //calling the 'do' function before its declation , no  problem !

			function do(){}

		}

		// how it will become after interpretation, it will be hoisted , like this
		function hoiz(){
			function do(){} //the function declation is moved to the top
			do(); //calling the 'do' function before its declation , no  problem !

		}

	```	

   But there is an excpetion to this rule , the function expression declarted with var are not hoisted !
   Consider this example



	```javascript
		function hoiz(){
			do(); //calling the 'do' function before its declation , Error cause the function is declared as var expression

			var do = function (){} //declare a function as expression

		}

		// what a compiler see  , the declaration will be hoisted but without initialization and definition
		function hoiz(){&
			var do;
			do();
			do = function(){}
		}

	```
	variable declared with var keyword are hosted but not initialized

	```javascript
		function hoiz(){
			console.log(tmp);
			if(true){
				var tmp='tmpValue';
			}
		}

		// what a compiler see  , the declaration will be hoisted but without initialization and definition
		function hoiz(){&
			var tmp;
			console.log(tmp);  //undefined in this case cause not initialized
			if(true){
				tmp = 'tmpValue';
			}
			
		}

	```
	bind a function to current object in case of array method like forEach , map,  filter , ...
	
	```javascript
		var obj  = {
			name:'sorrow maker',
			arr:[1,2,3];
			describe:function(){
				this.arr.forEach(function(item){
						this.name // it will get 'sorrow maker' as value
					}, this) //this, used to link inside callback to the current object
			}
		}
	```

### Extract Method
	to extract a method from object and make it as a function , you can use bind methodto avoid error
	```javascript
		var obj = {
			name:'sorrow maker',
			describe:function(){
				return this.name;
			}
		}

		//linking without bind method
		var func =  obj.describe;
		func(); // TypeError cannot find property name , cause in this case this refer to the current call object , in our case its global or window 

		//linking using bind
		var func =  obj.describe.bind(obj);
		func() // will return 'sorrow maker'

	```

### Arguments objets

	arguments is an object created for each function adn it contains all function arguments  including the caller and the function name
	the structure of arguments object is like bellow:
		arguments {'0' :'firstparamvalue' , 
				   '1' : 'secondpraamvalue'}
	its important to note that , arguements are not an array , its an object with indices as keys ,and it has a length property
		
	to convert arguments object to an array you can use the code bellow:

	```javascript

		var arrArguments = [].slice().call(arguemnts);
		//Or
		Array.prototype.slice.call(arguements);

	```	

	to initalize the optional parameter :


	```javascript

		optionalParam = optionalParam || 0; // it give 0 as value to optional param if no value is specified

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



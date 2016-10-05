# Javascript Notes

	Collection of notes about javascript , useful to refresh  your memory ;)



			     _        _    __     __     _      ____      ____    ____                 ____    _____  
			  U |"| u U  /"\  u\ \   /"/uU  /"\  u / __"| uU /"___|U |  _"\ u     ___    U|  _"\ u|_ " _| 
			 _ \| |/   \/ _ \/  \ \ / //  \/ _ \/ <\___ \/ \| | u   \| |_) |/    |_"_|   \| |_) |/  | |   
			| |_| |_,-./ ___ \  /\ V /_,-./ ___ \  u___) |  | |/__   |  _ <       | |     |  __/   /| |\  
			 \___/-(_//_/   \_\U  \_/-(_//_/   \_\ |____/>>  \____|  |_| \_\    U/| |\u   |_|     u |_|U  
			  _//      \\    >>  //       \\    >>  )(  (__)_// \\   //   \\_.-,_|___|_,-.||>>_   _// \\_ 
			 (__)     (__)  (__)(__)     (__)  (__)(__)    (__)(__) (__)  (__)\_)-' '-(_/(__)__) (__) (__)



## Variable Initialization

allways use the keyword  'var' for the best practice ,  this keyword limit
the scope of the variable and prevent the variable to be setted in
undesirable location 


the type of variable is attributed by the VM (like google V8) in the
execution mode , by using the init value , the type will change if another
value is affatected to the variable.. , 

you can display the varibale type using the key word  ,  typeof 

```javascript
	var mystr = "string content";
	console.log(typeof mystr); // 'string'
``` 

## Browser 
 The objets bellow are specific to the brower you can not use them in node.js
```javascript
 	var value = prompt("enter your age , the default value is provided",30);
 	var isconfirmd = confirm("are you a programmer ?");
 ```

## Comparaison
when you compare to variable be aware of the automatic type convertion , for example

if("01" == 1)  , this will be true , cause the compiler convert to
appropriate type before comparing  ,  the same thing for this if (1 == true)
and so on ..


## Functions

 the function can be declared anywhere just like a variable and use reference to it

```javascript
	 var myf =  function(){};
 ```

 the function can be executed in the same place when its declared using the IIFE (Immediatly invocked function expression)
 
 ```javascript
  (function(){
  	console.log('this wilk be invocked immedialty');

  })();
 
``` 
	Get calling function and caller 
```javascript	
 arguments.callee.caller  //get reference to caller method
 arguments.callee.callee //get name of calling function
```

	Convert the arguments object to array
```javascript	
    //get values of otheres parameters
    var args = [].slice.call(arguments) // slice without parameters copies all
    console.log( args.join(':') ) // now .join works
```


## Arrays
 Some usefull array methods

	```javascript
 		 var arr =  ['f','i','j'];
		 arr.length //as property of Array
		 
		 arr.pop() // delete the last element and return it
		 arr.push('') // arr.push([]) // put values in array 


		 arr.shift() ; // delete the first element in the array and return it
		 arr.unshift('','',''); // add values to array starting from the first position
		 var str = arr.join(','); // return array values separated by ','
		 var arr = str.split(',') // create an  array
		 //NB :  push and pop is faster than shift unshift 

		 ar.splice(indexstart , nbelement , [elem1, elem2,..])
		 arr.splice(0,1) // delete one element starting from 0
		 arr.splice(0,1,'A','B'); // delete 1 element from 0 and insert A,B 
		 arr.splice(0,0,'A','B') // insert A, B in the position 0 without removing any element
		 //NB : any element , the index can be negative to start from end of array
		 var sub  =  arr.slice(0,2); //reurn array with two elments starting from 0
		 var sub = arr.slice(1) // return array with all elements starting from 1st position
		 arr.reverse() // reverse order
		 arr.sort()//sort by natural order
		 arr.sort(comp) ; 
		 function comp(a,b){...}

		 var ar =  new Array(5).join('a'); //create a string with 'aaaa' from array
```

## Strings

 initiaalisation of strings  :  
```javascript
 var str = "strig"  or var str = '' ;  or
 ```

	Some functions : 
    
```javascript
     
     str.toUpperCase()
     str.toLowerCase()
     str[positon] ;
     str.charAt(position);
     str.indexOf("stringforserach");
     str.subString(startPosition , endPosition);
     str.subStr(firstPosition , endPosition);
     str.slice(startposition , endpotiion ) we can use nagative value it
     will start from the end in this case 

```




## Numbers

```javascript
	 var s= 0/0 

	 if (NaN == NaN) //->  false
	 if (isNaN(s)) true // use isNaN to test your numbers

	   parseInt(str) 
	   parseFloat(str)
	 // implementing isNumber
	 function isNumber(n ){
	      return !isNaN(parseFloat(n)) && isFinite(n);
	 }

	 Math.round() //nearest
	 Math.floor() // lowest
	 Math.ciel() //highest
	 a.toFixed(2) // display 2 digits after "." or "," for precision

```

## Objects

  var animal  = {}
  var rabbit  = Object.create(animal) // rabbit.prototype = animal , the rabbit will get all animal properties
  Object.getPrototypeOf(rabit) === animal) // check if rabbit is a subclass , it will return true
  obj.hasOwnPorperty('name') // test id obj has given property  and not inherited




(C) Ali Amechghal  - MIT LICENCE

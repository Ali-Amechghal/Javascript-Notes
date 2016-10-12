# Speaking JS  (Part 2)

    List of notes and tricks exctracted from SpeakingJS Book , greate Boook by the way :)
    This part cover Functions

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
    the function declared as expression are not hoisted 
    ```javascript
        var fct = function(){} //functiion expression
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
    Some notes :
    - in javascript function arguments are optional
    - non given argument are considered 'undefined'
     
    - arguments is an object created for each function adn it contains all function arguments  including the caller and the function name
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
    If you change a parameter the equivalent property in arguments object will be changed , but not in strict mode

    You can use a named parameter , but using an object instead of separated parameters
        function iUseNamedParam({start:0 , step:1})

### IIFE (Immediatly invocked function expression)
    we can use IIFE to limit a scope of variables 
        ```javascript
            function test(){
                if(true){
                    (function(){
                        var localvar =''; //localvar is only known inside IIFE
                        }());
                }
            }
        ```
         * IIFE MUST be an expression 
         * Never forget ';' after IIFE , consider this example

         ```javascript
            (function first(){}())
            (function second(){}())
         ```
         The second function is used as an argument to the first function
     To use global object inside IIFE
        ```javascript
            (function (global){

                }(typeof winsow !== 'undefined' ? window : global));
              //window in browser , and global object in nodejs 
        ```     
## Environnement
    Environnement is a javascript data structure where variables are stored
    The Function record her scope in environnement variable [scope] and outer scope reference in [scope.outer]
## Objects and Inheritance
    
    ### Deleting property

    Deleting object property ; delete keyword doesn't act in prototype properties , only in object propoerties

        ```javascript
            delete obj.cannotBeDeleted //return false
            delete obj.doesnotExists //return true
            delete obj.canBeDeleted //return true

        ``
    ### Adding propoery

     In javascript , you can add property to already created object like this:
        ```javascript
            var obj = {}
            obj.addedPropoeryName='value';
            //or we can create and configure a property
            Object.defineProperty(obj , 'canBeDeleted',{
                 value:'my default value',
                 configurable:true/false //if its true we can delete it , false we cannot
                })
        ```

    ### Binding 
        We can bind a function to a given object, by using call or bind or apply methods

        ```javascript
            Function.prototype.call(objectContext, arg1, arg2);
            myObj.fct.call(newObject , 1, 2, 3);
            Function.prototype.appy(objectContext , arrayargs);
            myObj.fct.apply(newObject, [1,2])
            var newFct = Fct.bind(objctContext);

        ``` 
        NB : apply dont work with constructors; you can bypass it like this
        ```javascript
             var arr = [2016,7,15];
             var date =  new (Function.prototype.bind.apply(Date, [null].concat(arr));

        ``
    ### Object Wrapper
        ```javascript

            Object(undefined)  == {}
            Object(null) == {}
            Object(true/false) == new Boolean(true/false)
            Object(num) == new Number(num)
            Object(str) == new String(str);
            Object(obj) == obj //unchanged , we can use this wrapper to check if a given argument its an object
                function isObject(value){
                    return value === Object(value)
                }
    ### Prototype Relactionship
        ```javascript
            var person = {
                
                describe:function(){
                    return this.name;
                }
            }
            //create object that use person as super class and add properties
            var programmer=Object.create(person , {name:'Ali'});
            Object.getPrototypeOf(programmer) // will get person oject
            pereson.isPrototypeOf(programmer) // true

            //
            var a={}
            var b=Object.create(a);
            var c =Object.create(b);

            a.isPrototypeOf(b) //true
            a.isPrototypeOf(c) //true

        ```
    ### Properties
    define object properties 
        ```javascript
          //create an empty object with properties
            var instance = Object.create({} ,{
                name:{
                    value:'default name',
                    enumerable:true , //it can be listed with forEach
                }
                })
        ```
    listing object properties
      ```javascript
        //getting object and super object properties
        Object.keys(insance).forEach(function(element , index, array){
            });
        for (key in instance){}

        //getting object properties only
        Object.getOwnPropertyNames(object).forEach(function(element , index , arr){
                console.log(element);
            });
        //check if property bellown to the current object and not super object
        Object.hasOwnProperty(instance ,  property_name);
    ```
    When we create a propery with descriptor (defineProperty) , the property enumerable , configurable and writable are false





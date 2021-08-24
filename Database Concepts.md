## Database Concepts

* How to create database ?

   `````````````````
  database= firebase.database();
   `````````````````

  

* How to read data from database?

  > Reading data from database is retrieving the data stored in the database. We store data in JSON format (i.e {key:value pairs}). So each value stored in the database has particular key (node ) in the database. Whichever value we want to retrieve , we should refer to the associate key (node).. using ref function.  ref function takes three parameters.. event, function, error
  >
  > eg: var dbRef=database.ref(event,function,error)

  > ref creates a bridge from our application to the database node, whose value is required, and on that bridge we should create a listner which keeps listening changes in that node.. We want to capture all the value changes at that node .. so we write as follows
  >
  > ```````````````````````````
  > dbRef.on("value",readData,readError)
  > ```````````````````````````

  ​               

  > readData and readError are the functions which are called by the Value event automatically with all the data at the referred location 
  >
  > ``````````````````````javascript
  > function readData(data){
  >   var dbData= data.val();
  > }
  > ``````````````````````
  >
  > data -- all the data captured at the referred location is stored in this variable automatically
  >
  > val()-- this function retrieves all the data captured at the referred location. Usually this will be a json object consisting of key:value pairs.. 

  *  Read operation examples from asynchronus ball movement and car game 

    ````````````````````````javascript
    // asynchronus ball movement
    var positionRef= database.ref('ball/position');
    positionRef.on("value",readPosition)
    
    function readPosition(data){
    
        position=data.val();
    
        ball.x= position.x;
        ball.y= position.y;
    
    }
    
    // Game.js from car game
    
    getState(){
            var gameStateRef= database.ref('gameState');
        // function(data)-- is called anonymous function
            gameStateRef.on("value",function(data){
                gameState= data.val();
            })
        }
    
    ````````````````````````

    

      

  > Anonymous  functions are usually used when we are calling them from other functions and which are never called again from any parts of the application.  Anonymous functions have no name .. they have only function definition which describes the actions to be performed by them.

  

*  How to write data into the database?

  > Storing or updating data in database is called write operation . We always write data in JSON format that is key:value pairs.. 
  >
  > So, we need to refer to **one node** **higher**  , whenever we do write operation. 
  >
  > if the database nodes are as below 
  >
  > ![image-20210323060916354](C:\Users\Karthikeya\AppData\Roaming\Typora\typora-user-images\image-20210323060916354.png)
  >
  > 



> To update the gameState value, we need to refer one node higher than gameState, i.e database itself. 
>
> Database is called as root node and can be written as '/'.

``````````````````javascript
dbRef = database .ref('/')
``````````````````

> We should use either update or set functions on the reference object. Examples from our games
>
> `````````````````````````````````````javascript
> // asynchronous ball movement
> database.ref('ball/position').update({
>         x:position.x+x,
>         y:position.y+y
>       }
>     )
> 
> // car game
> 
> update(state){
>         database.ref("/").update({
>             gameState:state
>         })
>     }
> 
> `````````````````````````````````````
>
> 

 
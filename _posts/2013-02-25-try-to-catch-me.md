---
layout: post
title: "try to catch me"
description: ""
category: 
tags: ['javascript', 'code']
---
{% include JB/setup %}

Javascript try/catch blocks are pretty standard and straight forward. 

```javascript
try{
  // try some stuff and fail
  throw new Error('failsauce');
}
catch(error){
  console.log(error);
  // Error {
  //   name    : ErrorName,
  //   message : 'error message'
  // }
}
```

Note that the catch block passes in an `error` argument which you can then access
the error/exception's properties to learn more about what exactly when down.

## You're exceptional

You can `throw` your own custom Objects and then access their properties in the
`catch` block.

```javascript
try{
  throw {
    name    : 'FooError',
    message : 'foo message'
  };
}
catch(error){
  console.log(error);
  // Error {
  //   name    : FooError,
  //   message : 'foo error'
  // }
}
```

or another way

```javascript
function FooError(){
  this.name = 'FooError';
  this.message = 'foo message';
}
try{
  throw new FooError();
}
catch(error){
  console.log(error);
  // Error {
  //   name    : FooError,
  //   message : 'foo error'
  // }
}
```

## All together now

```javascript
function UserException(message){
  this.message = message;
  this.name = 'UserException';
}

function returnUser(userName){
  var users = {
    'cgcardona' : {
      fName : 'carlos',
      lName : 'cardona'
    }, 
    'sol' : {
      fName : 'soljah',
      lName : 'cardona'
    }, 
    'natalia': {
      fName : 'natalie',
      lName : 'cardona'
    }
  };
  if(users[userName] !== undefined)
    return users[userName];
  else {
    throw new UserException('User ' + userName + ' is not registered');
  }
}

try{
  var user = returnUser('natalia');
  console.log(user);
  // Object {fName: "natalie", lName: "cardona"} 

  var user = returnUser('foobar');
}
catch(e){
  console.log(e);
  // UserException {message: "User foobar is not registered", name: "UserException"} 
}
```

## More info

* [try/catch docs on Mozilla](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Statements/try...catch)
* [throw docs on Mozilla](https://developer.mozilla.org/en-US/docs/JavaScript/Reference/Statements/throw)

---
layout: post
title: "Sorting an array of integers"
description: ""
category: 
tags: ['javascript', 'code']
---
{% include JB/setup %}

In `javascript` so that odd numbers are on the left and even numbers are on the right:

	window.onload = function(){
	  function sortArr(theArray){
	          
	    var leftPointer = 0;
	    var rightPointer = theArray.length - 1;
	          
	    while(leftPointer < rightPointer) {
	            
	      if(((theArray[leftPointer] % 2) !== 0) && ((theArray[rightPointer] % 2) !== 0)){
	        leftPointer++;
	      }   
	      else if(((theArray[leftPointer] % 2) === 0) && ((theArray[rightPointer] % 2) !== 0) || ((theArray[leftPointer] % 2) === 0) && ((theArray[rightPointer] % 2) === 0)){
	          
	        var tmp1 = theArray[leftPointer];
	        var tmp2 = theArray[rightPointer];
	           
	        theArray[leftPointer] = tmp2;
	        theArray[rightPointer] = tmp1;
	      }   
	      else{
	        rightPointer--;
	      }   
	    }   
	        
	    return theArray;
	  }
	  console.log(sortArr([1,2,3,4,5,6]));
	  // returns [1, 5, 3, 4, 2, 6] 
	};

[Mike Sealand](https://github.com/msealand) came along with the following and destroyed me with regards to LOC. Also nice use of `.reduce` and `.concat`

    window.onload = function(){
      function sortArr(theArray) {
        var separatedArrays = theArray.reduce(function(result, value) {
          result[value%2].push(value);
          return result;
        }, [[],[]]);
        return separatedArrays[1].concat(separatedArrays[0]);
      }

      console.log(sortArr([1,2,3,4,5,6]));
      // returns [1, 3, 5, 2, 4, 6] 
    };

[@omniegg](https://twitter.com/omniegg) [weighed
in](https://twitter.com/omniegg/status/301576200592175104) with the following if
you have [underscore.js](http://underscorejs.org):

    window.onload = function(){
        console.log(_.sortBy([1,2,3,4,5], function(n){ return n%2 }));
    };

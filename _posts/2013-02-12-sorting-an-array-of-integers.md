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

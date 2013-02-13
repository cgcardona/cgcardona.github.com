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

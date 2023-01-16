---
title : Flatten a nested array using .reduce method in Javascript
description : Flatten a nested array using .reduce method in Javascript
tags : [tech,technology,javascript,node, array]
date : 2022-01-01
categories : [Technology, Javascript]
menu : main
---


    ```
    const arr = [[1],[2],[3],[[4,5],[6,7],[[8,9],[10,11],[12,13]]]];
    const initialValue = [];
    const flatten = (arr) => arr.reduce((flattened,toFlatten) => {
      return flattened.concat(Array.isArray(toFlatten) ? flatten(toFlatten): toFlatten);    
    }, []); 
    console.log(flatten(arr));
    ```


This is a very interesting one liner to flatten an array. We're using reduce method on the array and inside the reducer function, we check if the `toFlatten` argument is an array or not. If not, then we call the function recursively. 
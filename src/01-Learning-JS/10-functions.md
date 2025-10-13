# 1.9 JS Functions: Do One Thing Well

## Start Your GH Workflow

Remember, before you start anything else, always follow this GH methodological workflow:

1. Create meaningful **branch** that uses the agreed upon naming scheme: `CHP/X.x--lastname`.
2. Practice the iterative process to **commit** and **push** regularly with meaningful **commit messages**.

## Overview

We've learned a lot so far about JS: data primitives and types, operators, conditionals, loops and parsers, and other types of transformers. Now, one of the last fundamentals to learn about JS is the ability to wrap up some code that performs one functional action well.

<img src="./../assets/images/1-js/penguin-windup.jpg" style="width:200px;float:left;border-radius: 10px;margin-right:1rem">

A ***function*** is way of bundling up code to perform specific tasks. It's kind of like making a little JS wind-up toy that runs on command.

Functions are useful because they can help make your code more organized and save you from repetition. If you have to do some task over and over again, you don't want to write out the same code over and over again from scratch.  In other words, if you find yourself ... repeating yourself, it may makes sense to define *one function* that can take in the data as a parameter, then return the changed data to another spot in your program.

Functions in JS can get complex and nuanced, but let's focus on some fundamentals.

## 1.9.1 *Define* a Function

In the current standard of JS, a function is composed of a sequence of statements called the *function body*. Values can be passed to a function as *parameters*, and a function can, and normally should *return* a value.

Below is the basic structure of a basic function body using the arrow notation approach. Note how it:

1. Starts with instantiating a name as a constant: `const meaningfulFunctionName =`.
2. Parantheses provide a place for parameters scoped to use only inside the function body: `(param1, param2)`.
3. Arrow notation tells JS that the body of the function is coming next: ` => `.
4. Curly braces scope the opening and closing of the function body: `{ ... }`.
5. The last line of any function before it closes with the curly brace is its `return` statement: `return newData`.

<!-- Example JS function structure -->
```javascript
const meaningfulFunctionName = (param1, param2) => {
  // A silly example of doing something with the parameters
  let newData = param1 + param2

  // return the desired data
  return newData
}
```

## 1.9.2 *Use* a Function

So, how do you use this awesome new, custom windup function? Easy, you can ***call*** it once it has been defined.

Let's pretend I've defined `meaningfulFunctionName()` in my code already. Now, I can ***call*** and use the function as follows:

```javascript
let q = "Q: Having fun yet?"
let a = "\nA: Of course, Dr. Lindgren! This is all amazing!"
let data = meaningfulFunctionName(q, a)
// data == "Q: Having fun yet?\nA: Of course, Dr. Lindgren! This is all amazing!"
```

## 1.9.3 About Parameters

Each function parameter is a simple identifier that you can access in the local scope of the function body.

```javascript
const myFunc = (a, b, c) => {
  // You can access the values of a, b, and c here
}
// You cannot access a, b, or c here oustide of myFunc
```

## 1.9.4 About Return Statements

The `return` statement allows you to return an arbitrary value from a function. ***One function call can only return one value***. But, you can simulate the effect of returning multiple values by returning an object or array and destructuring the result.

<p class="warning">
  By default, if a function's execution doesn't end at a return statement, or if the return keyword doesn't have an expression after it, then the return value is undefined.
</p>

## 1.9.5 Best Practices for Functions

Functions in all programming languages typically are best written to perform one complete action well. This is also why functions only return one value. In other words, don't write functions that are Jacks of All Trades.

For example, it doesn't make sense to write a function that converts dates in your data AND convert all strings to lowercase characters. Those are distinct functions that should be written separately of each other.

Overall keep that rule-of-thumb in mind as you practice writing functions.

## Exercises

<p class="note--data">
  For our exercises, we will again use the randomly generated sample of 20000 <strong>absentee</strong> NC voter data from the 2024 election cycle. The original set has over 468000 rows, so I reduced it to a smaller number to balance computational performance without forsaking much of the distribution of the full dataset. The data has been anonymized.
</p>

## E1. Attach the dataset

Use D3.js `FileAttachment()` method below in VS Code. Remember that you'll need to write a relative path as a String parameter that helps the computer find where the CSV file is in relation to this particular page's file in the project tree.

<!-- Attach sampled NC voter data -->
```js
// Convert to `js` codeblock and attach sampled NC voter data file: nc_absentee_mail_2024_n20000.csv
const data = FileAttachment("./../data/nc-voters/nc_absentee_mail_2024_n20000.csv").csv({typed: true})
```

## E2. Convert String dates to Date() objects

**Goal**: Write a function that accepts any array of objects that can convert any of its String date fields to Date() objects as a new property in the object.

First outline your procedure with steps below.

1. Create a data parser with d3.utcParse for the Date object conversion
2. Bring in 'data' (the dataset we used FileAttachment for earlier) and use the map function to create a codeblock that achieves the intended goal (will convert to a more generalized function later)
3. Create a new property in the objects that uses String date fields; in this case, creating "ballot_req_dt_obj" from "ballot_req_dt" with dateParser 
4. Return the item (in this case, labeled "ballot") and execute the new code ("dataUpdated") to check that it works. It did! Remembered to use lowercase 'y' this time to get the correct dates
5. Convert the codeblock into a function using the correct structure (+ making the objects and parameters more generalized, i.e. "item" instead of "ballot")

Now, code!

```js
// Went over this in class with prof; can create a .map() procedure first and then wrap it in a function. Did this and had the basic structure of a function written down lower in the codeblock for easier conversation. 
let dateParse = d3.utcParse("%d/%m/%y")
const mapConvertedDateObject = (data, dateKey, extraKey) => {
  let newData = data.map(
  (item) => {
    let newKey = dateKey+extraKey
    item[newKey] = dateParse(item[dateKey])
    return item
  }
  )
  return newData
}
```
```js
// Carried over "data" again since that's what I used for the original codeblock I converted into a function; same with "ballot_rtn_dt" and "_obj" 
mapConvertedDateObject(data, "ballot_rtn_dt", "_obj")
```
```js
// Convert and output variable here
mapConvertedDateObject
```

<p class="codeblock-caption">
  E1 Interactive Output
</p>

## E3. Create Your Own Function (with Conditions)!

**Goal**: Write your own function using the 2024 absentee NC voter data. The only condition is to include conditions. `:-)`

First outline your procedure with steps below.

1. Declare a function for the race object of the ballots from the dataset 
2. Set my parameters (data, raceKey), which are the dataset and my race key 
3. Use .map() to access each ballot and set the format for my returned response
4. Return "Race listed on ballot is" + the listed race 
5. Declare the function code in a new codeblock
6. Declare my output variable in a third codeblock

Now, code!

```js
// Your function code goes here
const raceCategories = (data, raceKey) => {
  let raceDataMap = data.map(
    (ballot) => {
      ballot.raceFormat = ballot.raceKey
      return "Race listed on ballot is" + ballot.raceFormat 
    }
  )
  return raceDataMap
}
```

```js
// Your use of the function code goes here
raceCategories = (data, "race_obj")
```

<p class="codeblock-caption">
  E2 Interactive Output
</p>

```js
// Your output variable here
raceCategories
```

## Submission

1. Create a **PR** (**pull request**) and use the provided content in the template to start it.
2. Respond to your peers and comment on their work on at least one chapter..
3. Submit the PR link in Moodle, when you're ready.

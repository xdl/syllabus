![Lesson in review](https://img.shields.io/badge/status-review-orange.svg)

# JavaScript Core I - 3

* [Array properties](#array-properties)
* [Manipulating arrays](#manipulating-arrays)
* [Array methods](#array-methods)
* [Array map](#array-map)
* [Array forEach](#array-foreach)
* [Array filter](#array-find)
* [Array find](#array-find)

**Learning Objectives**

By the end of this class, you should be able to answer these questions:

* How do you use array methods and properties to manipulate arrays?
* How can you chain array methods?
* What is a callback and how do you use it?
* What is an anonymous function and how do you use it?

---

## Array properties

Arrays, like strings, have a `length` property.

You can check this by starting a node console in your terminal.

```sh
$ node
> let arr = [1, 2, 3];
undefined
> arr
[1, 2, 3]
> arr.length
3
```

## Manipulating arrays

You can **get** a single value out of an array using **bracket notation**.

```sh
$ node
> let ingredients = ["Flour", "Water", "Salt"];
undefined
> ingredients[0]
Flour
> ingredients[1]
Water
> ingredients.length
3
```

Did you notice how we use `[0]` to get the first value? In programming we count starting at zero.

> The number inside of the brackets is called an **index**. Index just means the position of the item within the array.

You can also **set** a value using bracket notation and an assignment operator (`=`).

```js
let scores = [80, 41, 47];

scores[2] = 29; // Change the last score
scores[3] = 51; // Add a new score
```

### Exercise (5 minutes)

* Create an array with the names of the people on your table
* `console.log` out the names and how many people are at the table
* Put someone from another table at the beginning of the array
* Add someone else to the end of the list

## Working with arrays
When working with lists it is often useful to manipulate, enhance, or search the information in that list.

Some examples of things you might want to do with a list of data:

* Only use the first 10 items in a list
* Get people from a list whose name starts with a `M`
* Find the first person in a list to be over 100 years old
* Arrange people in a list alphabetically
* Get the last 10 items in an array
* Add all the numbers up in a list
* Get all the cats in an array of animals
* From a list of numbers, add a `£` sign prefix
* Combine a list of romance films and thrillers

### Exercise (10 minutes)

Working as a group - use the [MDN documentation on arrays](https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Global_Objects/Array#Instance_methods) to see if you can find what methods might be useful to achieving the above examples.

## Array methods

Do you remember how strings have special functions called methods? Don't worry if not! Here's an example to jog your memory:

```sh
$ node
> let name = "Daniel";
undefined
> name.toLowerCase()
daniel
```

Arrays also have several methods that you can use.

### `.sort()`

_An array method that sorts the values in an array into ascending alphabetical or numerical order._

```js
let unorderedLetters = ["z", "v", "b", "f", "g"];
let orderedLetters = unorderedLetters.sort();

let unorderedNumbers = [8, 5, 1, 4, 2];
let orderedNumbers = unorderedNumbers.sort();

console.log(orderedLetters); // logs [ 'b', 'f', 'g', 'v', 'z' ]
console.log(unorderedLetters); // logs [ 'b', 'f', 'g', 'v', 'z' ]

console.log(orderedNumbers); // logs [ 1, 2, 4, 5, 8 ]
console.log(unorderedNumbers); // logs [ 1, 2, 4, 5, 8 ]
```

> When you call this array method it uses the array on the left side of the dot as an input, and it sorts that array also returning it. Note how both ordered and unordered arrays are sorted now!

### `.concat()`

_Adds (or concatenates) another value or array to the array._

```sh
$ node
> let arr = [1, 2, 3];
undefined
> arr.concat(4)
[1, 2, 3, 4]
> arr
[1, 2, 3]
```

Did you notice how calling the concat method did not change `arr`? This is because `concat`, like most array methods, returns a _new_ array, it does not alter the one you called the method on.

If you wan to use the array returned by calling `.concat()` you should store it in a new variable.

```js
let arr = [1, 2, 3];
let newArr = arr.concat(4);

console.log(newArr); // logs [1, 2, 3, 4]
```

### `.slice()`

_Returns a slice of the array._

You can tell `.slice()` where you want the slice to begin and end by passing it two parameters.

```sh
$ node
> let arr = [0, 1, 2, 3, 4]
undefined
> arr.slice(0, 2)
[0, 1]
> ["a", "b", "c", "d"].slice(1, 2)
['b']
```

### `.includes()`

_Returns true if a value is in the array._

```js
let mentors = ["Daniel", "Irini", "Ashleigh", "Rob", "Etzali"];

function isAMentor(name) {
  return mentors.includes(name);
}

console.log("Is Rukmuni a mentor?");
console.log(isAMentor("Rukmini")); // logs false
```

### `.join()`

_Returns all the array values joined together in a string. By default, this method takes no parameters and then the elements are divided with a comma `,`. If you provide it with a string parameter though, then it becomes the divider of the elements, like the example below:_

```sh
$ node
> ["H", "e", "l", "l", "o"].join();
'H,e,l,l,o'
> ["H", "e", "l", "l", "o"].join("--");
'H--e--l--l--o'
```

There is a string method `.split()`. In an interactive console try using the string `.split()` method and the array `.join()`. How could they work together?

### Exercise (10 minutes)

* Use the array of the people from your table
* Combine it with another array filled with the names from another table
* `console.log` the names in alphabetical order
* Create a new value with the 2nd, 3rd and 4th people in it
* Create a function that takes a `name` and an array of names and returns a string. If the name is not in an array, it should retuern `<name> is not sitting at the table with <people in the array>`. If the name is in the array, it should return `<name> is sitting at the table with <people in the array>`.

## Array map

Imagine you have an array of names...

```sh
let mentors = ["Daniel ", "irina ", " Gordon", "ashleigh "];
```

You notice that he names are not formatted consistently. To fix the array you decide you need to trim whitespace and convert to lowercase. How do you do that for every value in the array?

We can write a function that changes one name:

```js
function tidy(name) {
  return name.trim().toLowerCase();
}
```

All you need to run every name in the array through this function and update the array values. Thankfully there is an array method that does just this!

### `.map()`

_Runs every item in the array through a function and returns a new array with the values returned by the function_.

Have a look at this other example:

```js
function double(number) {
  return number * 2;
}

let numbers = [1, 2, 3];
let numbersDoubled = numbers.map(double);
```

The `map()` method runs the function we provided (`double`) on each item in the array and uses the return values to create a new array. In the example `numbersDoubled` is a new array containing `[2, 4, 6]`.

### Callback functions

A function that we provide to a method is commonly called a _callback_ function. The term highlights that although we _provide_ the `double` function, the `.map()` method _calls_ it. (Notice how we never write `double()` to call the function).

We'll see callback functions used a lot more in the coming weeks. 

Often, when a function is only needed for a map operation, developers will declare the callback function inside of the method call. Let's try copying and pasting the function declaration inside of the `.map()` method call.

```js
let numbers = [1, 2, 3];
let numbersDoubled = numbers.map(function double(number) {
  return number * 2;
});
```

We can make this shorter by removing the function name to declare an _anonymous function_. We can do this because we are not using the function anywhere else in the code, so we do not need the function name to reference it.

```js
let numbers = [1, 2, 3];
let numbersDoubled = numbers.map(function (number) {
  return number * 2;
});
```

We can make this code even shorter still. In the latest versions of JavaScript a way of declaring functions was introduced called _arrow functions_. 

```js
let numbers = [1, 2, 3];
let numbersDoubled = numbers.map(number => {
  return number * 2;
});
```

The arrow function syntax lets you declare a function without the `function` keyword. (There are some other subtle differences between arrow functions and regular functions that you will learn about at a much later stage).

There is one last thing you can do to make your code shorter. If you remove the braces (`{}`) from an arrow function, the body of the function will be returned without needing to write the `return` keyword.

```js
let numbers = [1, 2, 3];
let numbersDoubled = numbers.map(number => number * 2);
```

In the example above, the expression `number * 2` is automatically returned because it comes directly after the `=>` arrow (instead of coming after curly braces). This is called an `implicit return`.

### Exercise (10 minutes)

I have a function defined below as:

```js
function abracaFunction(yourFunc) {
  console.log("I am abracaFunction! Watch as I mutate an array of strings to your heart's content!")
  const abracaArray = ['James', 'Elamin', 'Ismael', 'Sanyia', 'Chris', 'Antigoni']

  const abracaOutput = yourFunc(abracaArray)

  return abracaOutput
}
```

This function does not need to be modified. Can you pass in a _callback function_ which will mutate `abracaArray` such that it:

* Upper cases all letters in the array
* Sorts `abracaArray` in alphabetical order

### Exercise (10 minutes)

* Create a function that takes a `birthYear`, and returns the age of someone
* With an array of ages, create another array filled with their birth years `[ 1964, 2008, 1999, 2005, 1978, 1985, 1919 ]`
* `console.log` the birth years array

## Array forEach

The `.forEach()` method is similar to `.map()` except it does not return a new array. Therefore `.forEach()` is only useful if you want to perform _side effects_.

### Side effects

Generally, functions should take an input and return an output (based on that input), and not do anything else.

When functions meet this criteria they can be called _pure functions_.

A pure function does not:

* access any data unless it was passed in as a parameter
* change data declared outside the function
* interacts with anything outside of the function (e.g. logs a message to the console, shows a message on a website, saves data to disk)

These are all example of _side effects_. Of course, from time to time, we will need to perform side effects, but we should try to avoid side effects inside of functions and only have them when absolutely necessary.

### `.forEach()`

Say we want to log to the console a list of names.

```js
let names = ["Daniel", "mozafar", "irina"];
```

We can use `.forEach()` to go through the array, item by item, and call a function we provide.

```js
names.forEach(function(name, index) {
  console.log(index + ": " + name);
});
```

This logs each name to the console as hoped, but we notice that the names are not formatted correctly. You might be tempted to format the name inside of the `forEach` function.

However, it is good practise to write small functions with a single responsibility. So instead, we can write a `formatName` function (which we can re-use in other places) and pass it to `.map()` before calling `.forEach()`.

```js
function formatName(name) {
  return name.split("")[0].toUpperCase() + name.slice(1);
}

names.map(formatName).forEach(function(name, index) {
  console.log(index + ": " + name);
});
```

### Exercise (5 minutes)

You can drive in the UK at the age of 17.

* Write another function that takes a birth year and returns a string `Born in {year} can drive` or `Born in {year} can drive in {x} years`
* Use the array of birth years, `[ 1964, 2008, 1999, 2005, 1978, 1985, 1919 ]`, to get an array of strings saying if these people can drive
* `console.log` the answers

## Array filter

Imagine you have an array of students' test scores:

```js
let testScores = [90, 50, 100, 66, 25, 80, 81];
```

You want to show only the test scores that are higher than 80. How do you do that for every value in the array?

We can write a function that checks if one score is greater than 80:

```js
function isHighScore(score) {
  return score > 80;
}
```

To find out which scores were greater than 80, you'd have to run this function against every score in the array, and push the 80+ scores into a new array. Thankfully there is an array method that does just this!

### `.filter()`

_Runs every item in the array through a condition that we set, and returns a new array with the values that match the condition_.

```js
let highTestScores = testScores.filter(isHighScore);

console.log(highTestScores); // logs [90, 100, 81]
```

### Exercise (10 mins)

Create a function which:
* Takes an array of `birthYears`
* Uses `console.log` to print the message `These are the birth years of people who can drive: <filtered birth years>`
* Returns an array of people who can drive (remember, you can drive if you are 17 years or older)

## Array find

Imagine you have an array of names:

```js
let names = ["Daniel", "James", "Irina", "Mozafar", "Ashleigh"];
```

How would you find the first name that's longer than 6 characters?

You can write a predicate function that checks if a string is longer than 6 characters:

```js
function isLongName(name) {
  return name.length > 6;
}
```

To find the first item that satisfies the predicate you would have to go through each array item, and pass it into `isLongName`. Once it returns true, we can stop going through the array and grab the item that passed the predicate's test. Sounds complicated! Thankfully there is an array method that does just this!

### `.find()`

_Searches through the array and returns the value of the first item that satisfies a predicate function._

```js
let longName = names.find(isLongName);

console.log(longName); // logs Mozafar
```

### Exercise (10 mins)

Create a function which:

* Takes an array of names
* Looks to see if your name is in the array
* If it is, return `Found me!`; if not, return `Haven't found me :(`

### Chaining

Notice how we were able to write one method after another e.g. `names.map(formatName).forEach(log)`? This is called _method chaining_.

You can call `.forEach()` after `.map()` because `.map()` returns a new array.

Consider this code:

```js
function formatName(name) {
  return name.split("")[0].toUpperCase() + name.slice(1);
}

function log(name, index) {
  console.log(index + ": " + name)
}

let namesFormatted = names.map(formatName);
namesFormatted.forEach(log);
```

It can be written more simply (without assigning the array returned from `.map()` to a variable):

```js
names.map(formatName).forEach(log);
```

Be careful though! You can not call `.map()` after `.forEach`.

```js
names.forEach(log).map(formatName); // ERROR
```

This code does not work because `forEach()` does not return a new array (it returns `undefined`). The code is therefore attempting to call `.map()` on `undefined`, and `undefined` does not have a `.map()` method.

### Exercise (15 minutes)

Create a function which accepts an array of "messy" strings. Example:

```js
[100, 'iSMael', 55, 45, 'sANyiA', 66, 'JaMEs', 'eLAmIn', 23, 'IsMeal', 67, 19, 'ElaMIN']
```

This function should:

* Remove all non-string entries
* Only upper case the first letter of all strings and add an exclamation mark to the end

If you're using the above example, you should expect to return an array with 2x `Elamin!`, 1x `Sanyia!`, 2x `Ismael!` and 1x `James!`.

{% include "./homework.md" %}

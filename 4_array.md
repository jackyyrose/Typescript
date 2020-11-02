# Array Type Annotations
```javascript
let names: string[] = ['Danny', 'Samantha'];

let names: Array<string> = ['Danny', 'Samantha'];
> An alternative method is to use the Array<T> syntax, 
where T stands for the type.
```

```javascript
let names: string[] = [1,2,3]; // Type Error!

let names: string[] = ['Damien'];
names.push(666) // Type Error!
```

# Multi-dimensional Arrays
> We can also declare multidimensional arrays: arrays of arrays (of some type).
```javascript
let arr: string[][] = [['str1', 'str2'], ['more', 'strings']];

```

> Think of the string[][] above as short for (string[])[], that is, an array where every element has type string[].

> The empty array ([]) is compatible with any array type:
```javascript
let names: string[] = []; // No type errors.
let numbers: number[] = []; // No type errors.
names.push('Isabella');  
numbers.push(30);
```


# Tuples
> we’ve looked at arrays with all elements of the same type. JavaScript arrays are flexible and can have elements of different types. With TypeScript, we can also define arrays with a fixed sequence of types:

```javascript
let ourTuple: [string, number, string, boolean] = ['Is', 7 , 'our favorite number?' , false]; 
```

> In TypeScript, when an array is typed with elements of specific types, it’s called a tuple.

```javascript
let numbersTuple: [number, number, number] = [1,2,3,4]; // Type Error! numbersTuple should only have three elements.
let mixedTuple: [number, string, boolean] = ['hi', 3, true] // Type Error! The first elements should be a number, the second a string, and the third a boolean.
```

> As far as JavaScript is concerned, tuples act just like arrays. They both have .length properties. We can access (or change) the elements of both using [index]. But despite their similarities, tuples and arrays do not have compatible types within TypeScript. Specifically, we can’t assign an array to a tuple variable, even when the elements are of the correct type:

```javascript
let tup: [string, string] = ['hi', 'bye'];
let arr: string[] = ['there','there'];
tup = ['there', 'there']; // No Errors.
tup = arr; // Type Error! An array cannot be assigned to a tuple.
```

# Array Type Inference
> TypeScript can infer variable types from initial values and return statements. Even still, we may not know exactly what type inference to expect when dealing with arrays. For example:
```javascript
let examAnswers= [true, false, false];

```
> What is the type of examAnswers? It seems it could equally well be boolean[] or [boolean, boolean, boolean]. In reality, it is always the first of these, since this is the less restrictive type. This enables us to expand the array:
```javascript
examAnswers[3] = true; // No type error.

```
Since tuples have fixed lengths, we wouldn’t be able add additional boolean elements to a tuple:
```javascript
let tupleOfExamAnswers: [boolean, boolean, boolean] = [true, false, false];
tupleOfExamAnswers[3] = true; // Type error! The tuple only has 3 elements.
```

> We also get the same kind of type inference when we use the .concat() method:

```javascript
let tup: [number, number, number] = [1,2,3];
let concatResult = tup.concat([4,5,6]); // concatResult has the value [1,2,3,4,5,6].
```
> In the code above, TypeScript infers the variable concatResult as an array of numbers, not a tuple.

> The takeaway here is that type inference returns arrays. When we want tuples, we need to use explicit type annotations.


# Rest Parameters
> Assigning types to rest parameters is similar to assigning types to arrays. Here’s a rest parameter example without types:

```javascript
function smush(firstString, ...otherStrings){
  let output = firstString;
  for(let i = 0; i < otherStrings.length; i++){
    output = output.concat(otherStrings[i]);
  }
  return output;
}
```

> This function concatenates all of its arguments. For example, calling: smush('hi ', 'there') returns the value 'hi there'.” The rest parameter otherStrings lets the function work with any number of parameters greater than zero:

```javascript
smush('a','h','h','H','H','H','!','!'); // Returns: 'ahhHHH!!'.

```

> The function works well, but it is not type safe. We don’t want a misguided coder to make a mistake like smush(1,2,3), when that would cause an error. TypeScript to the rescue! Type annotations for a rest parameter are identical to type annotations for arrays. The function with a correctly typed rest parameter is then:

```javascript
function smush(firstString, ...otherStrings: string[]){
  /*rest of function*/
}
```

> With this change, TypeScript will treat otherStrings as an array of strings. This means that smush(1,2,3) will result in a type error because [2,3] is not an array of strings.



# Spread Syntax ( use ... to expand an array as elements)
> Like the finest wines and cheeses, TypeScript’s tuples pair beautifully with JavaScript’s spread syntax. This is most useful for function calls that use lots of arguments, like this:

```javascript
function gpsNavigate(startLatitudeDegrees:number, startLatitudeMinutes:number, startNorthOrSouth:string, startLongitudeDegrees: number, startLongitudeMinutes: number, startEastOrWest:string, endLatitudeDegrees:number, endLatitudeMinutes:number , endNorthOrSouth:string, endLongitudeDegrees: number, endLongitudeMinutes: number,  endEastOrWest:string) {
  /* navigation subroutine here */
}

let codecademyCoordinates: [number, number, string, number, number, string] = [40, 43.2, 'N', 73, 59.8, 'W'];
let bermudaTCoordinates: [number, number, string, number, number, string] = [25, 0 , 'N' , 71, 0, 'W'];

gpsNavigate(...codecademyCoordinates, ...bermudaTCoordinates);
// And by the way, this makes the return trip really convenient to compute too:
gpsNavigate(...bermudaTCoordinates, ...codecademyCoordinates);
// If there is a return trip . . . 


```

```javascript
function performDanceMove(moveName:string, moveReps:number, hasFlair:boolean):void{
  console.log(`I do the ${moveName} ${moveReps} times !`);
  if(hasFlair){
    console.log('I do it with flair!');
  }
}

let danceMoves:[string, number, boolean][] = [
  ['chicken beak', 4, false],
  ['wing flap', 4, false],
  ['tail feather shake', 4, false],
  ['clap', 4, false],
  ['chicken beak', 4, true],
  ['wing flap', 4, true],
  ['tail feather shake', 4, true],
  ['clap', 4, true],
];

for(let i=0;i<danceMoves.length; i++){
  performDanceMove(...danceMoves[i]);
}

```


> Review
* The type annotations for arrays.
* What tuples are, and how to do their type annotations.
* How type inference works with arrays and tuples.
* How to use the rest and spread operators with TypeScript.
> Arrays types are a crucial component of TypeScript
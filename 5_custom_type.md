# Custom types

> To define custom types in TypeScript. These include enums, generics, and object types. You will also learn to give convenient names to your types using type aliases.

> Pre-defined types can also be combined into custom types. Custom types are like fully assembled meals (pickles, as well as cheese, bread, and burger patties).

> The complex types covered here will be usable in the same ways as the simpler types covered earlier. They can be used as type annotations during variable declaration:

```javascript
let myVar: compType; 
```
> And they can be used as type annotations for functions:
```javascript
function testFn(param: compType): returnedCompType {
  /*Function body*/
}
```

> And you can even do type inference with complex types:
```javascript
let inferredTypeVariable = testFn(myVar);
// The variable inferredTypeVariable will have the type returnedCompType. 
```


# enum

```javascript
enum Direction {
  North,
  South,
  East,
  West
}

let whichWayToArcticOcean: Direction;
whichWayToArcticOcean = Direction.North; // No type error.
whichWayToArcticOcean = Direction.Southeast; // Type error: Southeast is not a valid value for the Direction enum.
whichWayToArcticOcean = West; // Wrong syntax, we must use Direction.West instead. 


```

```javascript
enum Direction {
  North = 8,
  South = 2,
  East = 6,
  West = 4
}

```

```javascript
let petOnSale = 'chinchilla';
let ordersArray = [
  ['rat', 2], 
  ['tarantula', 1], 
  ['hamster', 2], 
  ['chinchilla', 50]
];

// Write your code below:

enum Pet {
  Hamster,
  Rat,
  Chinchilla,
  Tarantula
}

let petOnSaleTS: Pet = Pet.Chinchilla;
let ordersArrayTS:[Pet, number][] = [
  [Pet.Rat, 2],
   [Pet.Tarantula, 1], 
  [Pet.Hamster, 2], 
  [Pet.Chinchilla, 50]
];


ordersArrayTS.push([Pet.Jerboa,3]);
//index.ts:27:25 - error TS2339: Property 'Jerboa' does not exist on type 'typeof Pet'.

```


# String Enums vs. Numeric Enums

> TypeScript also allows us to use enums based on strings, referred to as string enums. They are defined very similarly:
```javascript
enum DirectionNumber { North, South, East, West }
enum DirectionString { North = 'NORTH', South = 'SOUTH', East = 'EAST', West = 'WEST' }

```

> With numeric enums, the numbers could be assigned automatically, but with string enums we must write the string explicitly, as shown above. Technically, any string will do: North = 'JabberWocky' is a valid value definition. However, it is much better to use the convention shown here (North = 'NORTH'), where the string value of the enum variable is just the capitalized form of the variable name. This way, error messages and logs will be much more informative.

> We recommend to always use string enums because numeric enums allow for some behaviors that can let bugs sneak into our code. For example, numbers can be assigned directly to numeric enum variables:

```javascript
let whichWayToAntarctica: DirectionNumber;
whichWayToAntarctica = 1; // Valid TypeScript code.
whichWayToAntarctica = DirectionNumber.South; // Valid, equivalent to the above line.
```
> Strangely, even assigning arbitrary numbers, as in whichWayToAntarctica = 943205, will not lead to type errors.

> String enums are much more strict. With string enums, variables cannot be assigned to strings at all!

```javascript
let whichWayToAntarctica: DirectionString;
whichWayToAntarctica = '\ (•◡•) / Arbitrary String \ (•◡•) /'; // Type error!
whichWayToAntarctica = 'SOUTH'; // STILL a type error!
whichWayToAntarctica = DirectionString.South; // The only allowable way to do this.
```

> example
```javascript
let petOnSale = 'chinchilla';
let ordersArray = [
  ['rat', 2], 
  ['chinchilla', 1], 
  ['hamster', 2], 
  ['chinchilla', 50]
];

// Write your code below:
enum Pet {
  Hamster = 'HAMSTER',
  Rat = 'RAT',
  Chinchilla = 'CHINCHILLA',
  Tarantula = 'TARANTULA'
}

const petOnSaleTS : Pet = Pet.Chinchilla;

let ordersArrayTS : [Pet, number][] = [
  [Pet.Rat, 2], 
  [Pet.Chinchilla, 1], 
  [Pet.Hamster, 2], 
  [Pet.Chinchilla, 50]
];

ordersArrayTS.push(['HAMSTER', 1]);
//index.ts:26:21 - error TS2322: Type '"HAMSTER"' is not assignable to type 'Pet'.
//26 ordersArrayTS.push(['HAMSTER', 1]);
```

# Object Types

```javascript
let aPerson: {name: string, age: number};

aPerson = {name: 'Aisle Nevertell', age: "wouldn't you like to know"}; // Type error: age property has the wrong type.
aPerson = {name: 'Kushim', yearsOld: 5000}; // Type error: no age property. 
aPerson = {name: 'User McCodecad', age: 22}; // Valid code. 

```
> TypeScript places no restrictions on the types of an object’s properties. They can be enums, arrays, and even other object types!
```javascript


let aCompany: {
  companyName: string, 
  boss: {name: string, age: number}, 
  employees: {name: string, age: number}[], 
  employeeOfTheMonth: {name: string, age: number},  
  moneyEarned: number
};
```

```javascript
function sayHappyBirthdayWithObject(personObject: {name: string, age: number, giftWish: string, success: boolean}){
  let output ='';
  output += 'Happy Birthday '
         + personObject.name + '! ';
  output += 'You are now ' 
         + personObject.age + ' years old! ';
  output += 'Your birthday wish was to receive ' 
         + personObject.giftWish 
         + '. And guess what? You will ';
  if (!personObject.success){
    output += 'not ';
  }
  output += 'receive it! \n';
  console.log(output);
}

let birthdayBabies: {name: string, age: number, giftWish: string, success: boolean}[] = [
  {name: 'Liam', age: 0, giftWish: 'karate skills', success: false}, 
  {name: 'Olivia', age: 0, giftWish: 'a bright future', success:true}, 
  {name: 'Ava', age: 0, giftWish: '$0.25', success:true}
]; 

birthdayBabies.forEach(sayHappyBirthdayWithObject);

```

# Type Aliases

```javascript
type Person = {name:string, age:number};
let aCompany: {companyName: string, boss: Person, employees:Person[], employeeOfTheMonth: Person,  moneyEarned: number};


type Coord =  [number, number, string, number, number, string];

let codecademyCoordinates:Coord = [40, 43.2, 'N', 73, 59.8, 'W'];
let bermudaTCoordinates: Coord = [25, 0 , 'N' , 71, 0, 'W'];

```




# Function Types

> functions can be assigned to variables

```javascript
let myFavoriteFunction = console.log; // Note the lack of parentheses.
myFavoriteFunction('Hello World'); // Prints: Hello World
```

> we can precisely control the kinds of functions assignable to a variable. We do this using function types, which specify the argument types and return type of a function. Here’s an example of a function type that is only compatible with functions that take in two string arguments and return a number.

```javascript
type StringsToNumberFunction = (arg0: string, arg1: string) => number;
```
> the return type is number. Because this is just a type, we did not write the function body at all. A variable of type StringsToNumberFunction can be assigned any compatible function:

```javascript
let myFunc: StringsToNumberFunction;
myFunc = function(firstName: string, lastName: string) {
  return firstName.length + lastName.length;
};

myFunc = function(whatever: string, blah: string) {
  return whatever.length - blah.length;
};
// Neither of these assignments results in a type error.
```

> As we can see above, it doesn’t matter what we name the function parameters, so long as they have the correct types (string and string). Therefore, it doesn’t matter what we name the parameters in the type annotation (above, we chose arg0 and arg1).

> There’s something * important * to remember here. We must never be tempted to omit the parameter names or the parentheses around the parameters in a function type annotation, even if there is only one parameter. This code will not run!
```javascript
type StringToNumberFunction = (string)=>number; // NO
type StringToNumberFunction = arg: string=>number; // NO NO NO NO
```

> Function types are most useful when applied to * callback functions *. With how common callback functions are, it’s useful to know how to type them appropriately.

```javascript
// Math Operations
function add(a, b){return a+b }
function subtract(a, b){return a-b }
function multiply(a, b){return a*b}
function divide(a, b){return a/b}
function wrongAdd(a, b){return (a+b)+''}

// Add your function type below:
type OperatorFunction = (p1: number, p2: number)=> number;

// Math Tutor Function That Accepts a Callback
function mathTutor(operationCallback: OperatorFunction) {
  console.log("Let's learn how to", operationCallback.name,'!');
  let value25 = operationCallback(2,5);
  console.log('When we', operationCallback.name, '2 and 5, we get', value25, '.');
  console.log('When we', operationCallback.name, value25, 'and 7, we get', operationCallback(value25,7), '.');
  console.log('Now fill out this worksheet.');
}

// Call your functions below:
mathTutor(multiply);
mathTutor(wrongAdd);
//index.ts:22:11 - error TS2345: Argument of type '(a: any, b: any) => string' is not assignable to parameter of type 'OperatorFunction'.
//  Type 'string' is not assignable to type 'number'.

// 22 mathTutor(wrongAdd);
```



# Generic Types

> Generics give us the power to define our own collections of object types. Here’s an example:
```javascript
type Family<T> = {
  parents: [T, T], mate: T, children: T[]
};
```

> This code defines a collection of object types, with a different type for every value of T. The generic Family<T> cannot actually be used as a type in a type annotation. Instead, we must substitute T with some type of our choosing, for example string. Then, Family<string> is exactly the same as the object type given by setting T to string: {parents:[string,string], mate:string, children: string[]}. So the following assignment will be error free:

```javascript
let aStringFamily: Family<string> = {
  parents: ['stern string', 'nice string'],
  mate: 'string next door', 
  children: ['stringy', 'stringo', 'stringina', 'stringolio']
}; 
```

> In general, writing generic types with type typeName<T> allows us to use T within the type annotation as a type placeholder. Later, when the generic type is used, T is replaced with the provided type. (Writing T is just a convention. We could just as easily use S or GenericType. )

```javascript
type Human = {name: string, job: string};
type Dog = {name: string, tailWagSpeed: number};

type Family<T> = {
  parents: [T, T], mate: T, children: T[]
};
//Do not change the code above this line.

//Provide type annotations for the variables below:
let theFamily: Family<number> = {
  parents: [3, 4], mate: 9, children: [5, 30, 121]
};

let someFamily: Family<boolean> = {
  parents: [true, true], mate: false, 
  children: [false, false, true, true]
};

let aFamily: Family<Human> = {
  parents: [
    {name: 'Mom', job: 'software engineer'},
    {name: 'Dad', job: 'coding engineer'}
  ],
  mate: {name: 'Matesky', job: 'engIn general, writing generic types with type typeName<T> allows us to use T within the type annotation as a type placeholder. Later, when the generic type is used, T is replaced with the provided type. (Writing T is just a convention. We could just as easily use S or GenericType. )ineering coder'},
  children: [{name: 'Babesky', job: 'none'}]
};

let anotherFamily: Family<Dog> = {
  parents: [
    {name: 'Momo', tailWagSpeed: 3},
    {name: 'Dado', tailWagSpeed: 100}
  ],
  mate: {name: 'Cheems', tailWagSpeed: 7},
  children: [
    {name: 'Puppin', tailWagSpeed: 0.001},
    {name: 'Puppenaut', tailWagSpeed: 0.0001},
    {name: 'Puppenator', tailWagSpeed: 0.01}
  ]
};

```



# Generic Functions

```javascript
function getFilledArray<T>(value: T, n: number): T[] {
  return Array(n).fill(value);
}
```

> The above code tells TypeScript to make sure that value and the returned array have the same type T. When the function is invoked, we will provide T‘s value. For example, we can invoke the function using getFilledArray<string>('cheese', 3), which sets T equal to string. This still evaluates to ['cheese', 'cheese', 'cheese'], but the function is now correctly typed and less prone to errors. The function getFilledArray<string> is precisely the same as if we had written (value: string, n: number): string[] in its type annotation.

> In general, writing generic functions with function functionName<T> allows us to use T within the type annotation as a type placeholder. Later, when the function is invoked, T is replaced with the provided type.

> example: Use the function getFilledArray<T>() to assign values to the variables stringArray, numberArray, personArray, and coordinateArray.

Write your code so that:

Each value should be an array of 6 elements.
All elements in stringArray should equal 'hi'.
All elements in numberArray should equal 9.
All elements in personArray should equal {name: 'J. Dean', age: 24}.
All elements in coordinateArray should equal [3,4].
Don’t forget to specify the value of T!

```javascript
function getFilledArray<T>(value: T, n: number): T[] {
  return Array(n).fill(value);
}

let stringArray: string[];
let numberArray: number[];
let personArray: {name: string, age: number}[];
let coordinateArray: [number, number][];

// Write your code below:
type Person = {name: string, age:number};
stringArray = getFilledArray<string>('hi',6);
numberArray = getFilledArray<number>(9,6);
personArray = getFilledArray<Person>({name:'J. Dean', age: 24}, 6);
coordinateArray = getFilledArray<[number,number]>([3,4],6);

```

# Review
> Upon completion of this lesson you have officially* become a TypeScript Hero. No longer are you limited to TypeScript’s pre-defined types; you have now learned how to create your own custom types! These include:

+ Enums (both string and numeric)
+ Object types
+ Function types
+ Furthermore, you learned how to refer to complex types using type aliases. And you even learned to master generics, which are like doubly-custom types. Impressive!
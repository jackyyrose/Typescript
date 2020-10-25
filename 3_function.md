# Parameter Type Annotations

> The type annotations ensure that the parameters are of the correct type:

```javascript
    function greet(name: string) {
      console.log(`Hello, ${name}!`);
    }
    greet('Katz'); // Prints: Hello, Katz  
    greet(1337); // Error: argument '1337' is not assignable to parameter of type 'string'
```

> Parameters that we do not provide type annotations for are assumed to be of type any—the same way variables are.

```javascript
    function printKeyValue(key: string, value) {
        console.log(`${key}: ${value}`);
    }

    function triple(value:number) {
      return value * 3;
    }
    
    function greetTripled(greeting:string, value:number) {
      console.log(`${greeting}, ${triple(value)}!`);
    }
    
    greetTripled('Hiya', 5);
```


# Optional Parameters
> To indicate that a parameter is intentionally optional, we add a ? after its name. This tells TypeScript that the parameter is allowed to be undefined and doesn’t always have to be provided.
```javascript
function greet(name?: string) {
  console.log(`Hello, ${name|| 'Anonymous'}!`);
}

greet(); // Prints: Hello, Anonymous!
```

# Default Parameters

> If a parameter is assigned a default value, TypeScript will infer the variable type to be the same as the default value’s type. (This is similar to how TypeScript infers the type of an initialized variable to be the same as the type of its initial value.)

```javascript
function greet(name = 'Anonymous') {
  console.log(`Hello, ${name}!`);
}
```

> The function greet() can receive a ***string or undefined*** as its name parameter—if any other type is provided as an argument, TypeScript will consider that a type error.

> Parameters with default values don’t need a ? after their name, since assigning a default value ***already implies that they’re optional*** parameters.

```javascript
function proclaim(status="not ready...", repeat=1) {
  for (let i = 0; i < repeat; i += 1) {
    console.log(`I'm ${status}`);
  }
}

proclaim();
proclaim('ready?');
proclaim('ready!', 3);
```

# Inferring Return Types

>TypeScript can also infer the types of values returned by functions. It does this by looking at the types of the values after a function’s return statements.

```javascript
function ouncesToCups(ounces: number) {
  return `${ounces / 16} cups`;
}

const liquidAmount: number = ouncesToCups(3);
// Type 'string' is not assignable to type 'number'.
```



# Explicit Return Types

>If we’d like to be explicit about what type a function returns, we can add an explicit type annotation after its closing parenthesis. Here, we use the same syntax as other type annotations, a colon followed by the type. TypeScript will produce an error for any return statement in that function that doesn’t return the right type of value.

```javascript
function createGreeting(name?: string): string {
  if (name) {
    return `Hello, ${name}!`;
  }

  return undefined;
  //Typescript Error: Type 'undefined' is not assignable to type 'string'.
};
```


```javascript
const createArrowGreeting = (name?: string): string => {
    if (name) {
        return `Hello, ${name}!`;
    }

    return undefined;
    // Typescript Error: Type 'undefined' is not assignable to type 'string'.
};
```

# Void Return Type

> Type annotations are very useful and should always be used unless there’s a very good reason not to. They make everything neat and aid in understanding our code.

> For these reasons, it is often preferred to use type annotations for functions, **even when those functions don’t return anything**. Example:

```javascript
function logGreeting(name:string): void{
  console.log(Hello, ${name}!`)
}
```

# Documenting Functions
```javascript
/**
   * Returns the sum of two numbers.
   *
   * @param x - The first input number
   * @param y - The second input number
   * @returns The sum of `x` and `y`
   *
   */
  function getSum(x: number, y: number): number {
    return x + y;
  }
}
```

## Review
Learnt how to use TypeScript to specify the types of function parameters and return types. 

* Give type annotations to function parameters.
* Deal with type annotations for optional parameters, which may have default values.
* Understand how TypeScript determines the return type of a function.
* Explicitly specify return types for functions, including for functions that don’t return anything.
* Use the above skills to diagnose and fix bugs in our code.
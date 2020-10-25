# From JavaScript to TypeScript

Invented in 1995, JavaScript was designed as a small scripting language for simple web pages in browsers. It wasn’t until 1999 that JavaScript was capable of supporting the kinds of dynamic web pages we see today, and using JavaScript that way wasn’t common practice until 2005.

To serve its original use-case, JavaScript was designed to be very flexible and easy to use for small applications. These features make JavaScript a great first language to learn, but they also make it less-than-ideal for building larger-scale applications with hundreds or even thousands of files. Stricter programming languages will inform the developer when they change one area of code in a way that will break other areas. JavaScript will not, which often leads to unexpected behavior at runtime.

To address these shortcomings, Microsoft developed TypeScript and released publicly in 2012 to blend the flexibility of JavaScript with the advantages of a stricter language.

TypeScript is a programming language that adds types to JavaScript. It allows us to write JavaScript with a set of tools called a type system that can spot potential bugs in, clarify the structure of, and help refactor our code. In addition, TypeScript added newer JavaScript language features, such as arrow functions and classes, years before they were added to JavaScript officially.

## what is
    * .ts extension;
    * ts transcompiler check, display errors;
    * transcompiler output a  .js  file;
        use command: $ tsc
                    $ node xxx.js

## Type Inferences
    when we declare a variable with an initial value, the variable can never be reassigned a value of a different data type. This is an example of type inference: everywhere in our program, TypeScript expects the data type of the variable to match the type of the value initially assigned to it at declaration

## Type Shapes
    An object’s shape describes, among other things, what properties and methods it does or doesn’t contain.

    TypeScript’s tsc command will let you know if your code tries to access properties and methods that don’t exist:
    "MY".toLowercase();
    // Property 'toLowercase' does not exist on type '"MY"'.
    // Did you mean 'toLowerCase'?

    quickly locate bugs in our code.

## Any (type)
    let onOrOff;
    onOrOff = 1;
    onOrOff = false;

    typeScript considers it to be of type any, and, therefore, doesn’t produce an error when we change the variable’s assignment from a number value to a boolean value.

## Variable Type Annotations
    In some situations, we’d like to declare a variable without an initial value while still ensuring that it will only ever be assigned values of a certain type. If left as any, TypeScript won’t be able to protect us from accidentally assigning a variable to an incorrect type that could break our code.

    We can tell TypeScript what type something is or will be by using a type annotation.
    * appending a variable with a colon (:) and the type

    let mustBeAString : string;
    mustBeAString = 'Catdog';
    
    // Error: '1337' is not assignable to type 'string'
    mustBeAString = 1337;

    *Annotations making your code ugly or hard for others to understand?
        No, they get automatically removed when compiled to JavaScript.

# To recap:

TypeScript is a superset of JavaScript that adds types.
The type system refers to TypeScript’s understanding of how your code is meant to function: mainly what data types should be stored under your variables.
TypeScript expects the data type of the variable to match the type of the value initially assigned to it at its declaration—this is know as type inference.
An object’s shape describes, among other things, what properties and methods it does or doesn’t contain. TypeScript knows not only what type something is but also what shape that type has.
When it isn’t able to infer a type, TypeScript will consider a variable to be of type any.
Type annotations are little pieces of code that indicate what type a variable is meant to be.
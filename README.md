# Learning TypeScript

## Day 1: Introduction to TypeScript

### 1. What is TypeScript?

TypeScript is a typed superset of JavaScript that compiles to plain JavaScript. It adds static typing, which helps catch errors early during development, improving code quality and readability.

- **JavaScript vs TypeScript**: JavaScript is a dynamic language, meaning variables don't have fixed types. In contrast, TypeScript allows defining specific variable types, reducing bugs, and enhancing code maintainability.

- **Benefits of TypeScript**:
  - Type safety: Errors are caught at compile time rather than runtime.
  - Better tooling (e.g., IntelliSense, autocompletion, and refactoring tools in editors like VSCode).
  - Easier collaboration on larger projects.

### 2. Setting Up TypeScript

You can set up a TypeScript project in Node.js:

1. Install TypeScript globally:
   ```bash
   npm install -g typescript
   ```
2. Initialize a project:
   ```bash
   tsc --init
   ```
   This generates a tsconfig.json file, where you can configure options like target JavaScript version, module resolution, etc.
3. Create a .ts file (e.g., index.ts) and compile it:
   ```bash
   tsc index.ts
   ```
   This generates a compiled JavaScript file (index.js).

### 3. Type Annotations

Type annotations in TypeScript help define the expected type of variables and functions.

- **Basic Types**: TypeScript supports all primitive types of JavaScript: number, string, boolean, null, and undefined.

```typescript
let age: number = 25;
let name: string = "Suryansh";
let isStudent: boolean = true;
```

- **Arrays**: You can specify the type of array elements.

```typescript
let numbers: number[] = [1, 2, 3, 4];
```

- **Tuples**: Tuples allow you to create arrays with a fixed number of elements of different types.

```typescript
let person: [string, number] = ["Suryansh", 25];
```

### 4. Type Inference

TypeScript can automatically infer types from assigned values.

```typescript
let message = "Hello"; // inferred as string
```

In this case, you don’t need to explicitly declare the type.

### 5. Union Types and Literal Types

- **Union Types**: A variable can be of more than one type using the union operator |.

```typescript
let id: string | number = 123;
id = "ABC"; // both are allowed
```

- **Literal Types**: You can restrict a variable to specific literal values.

```typescript
let direction: "up" | "down" = "up"; // direction can only be "up" or "down"
```

## Test Sheet - Day 1

### Multiple Choice

1. What does TypeScript add to JavaScript?

   - More performance
   - **Static typing and type safety**
   - In-browser code compilation

2. Type inference in TypeScript means:
   - The developer must always specify the type of variables
   - **TypeScript automatically determines the type of variables**
   - Variables can have multiple types

### Short Answer

1. Write a TypeScript example where you declare a variable price as a number and an array of numbers.

   ```typescript
   let price: number = 100;
   let prices: number[] = [20, 30, 40];
   ```

2. Explain the difference between union types and literal types with examples.

   ```typescript
   // Union
   let data: string | null = ‘Bad data’;

   // Literal
   let direction: “north” | “south” | “east” | “west” = “east”;
   ```

### Coding Challenge

Write a TypeScript function describePerson that accepts a parameter name as string and age as number and returns a sentence like:
"Suryansh is 25 years old."
Include type annotations in the function.

```typescript
// solution

function describePerson(name: string, age: number) {
  return `${name} is ${age} years old`;
}
```

## Day 2: Advanced Types & Functions

### 1. Functions in TypeScript

Functions in TypeScript allow you to specify both parameter types and return types, ensuring type safety.

- **Basic function syntax** with type annotations:

  ```typescript
  function greet(name: string): string {
    return `Hello, ${name}!`;
  }
  ```

- **Optional Parameters**: Use `?` to mark a parameter as optional.

  ```typescript
  function greet(name: string, age?: number): string {
    return age ? `${name} is ${age} years old.` : `Hello, ${name}!`;
  }
  ```

- **Default Parameters**: You can set default values for parameters.

  ```typescript
  function greet(name: string = "Guest"): string {
    return `Hello, ${name}!`;
  }
  ```

### 2. Rest Parameters

Rest parameters allow a function to accept an unlimited number of arguments as an array.

```typescript
function sum(...numbers: number[]): number {
  return numbers.reduce((total, num) => total + num, 0);
}
```

### 3. Return Type Annotations

TypeScript can infer the return type, but you can explicitly define it as well.

```typescript
function add(a: number, b: number): number {
  return a + b;
}
```

### 4. Void, Never, and Unknown Types

- **Void**: Used when a function doesn’t return any value.

  ```typescript
  function logMessage(message: string): void {
    console.log(message);
  }
  ```

- **Never**: Represents a function that never returns (e.g., functions that throw errors or have infinite loops).

  ```typescript
  function throwError(message: string): never {
    throw new Error(message);
  }
  ```

- **Unknown**: The `unknown` type represents a value that could be of any type, but requires extra checks to operate safely. It’s safer than `any` because it forces you to narrow down the type before using it.

  ```typescript
  let input: unknown;
  input = "Hello";
  if (typeof input === "string") {
    console.log(input.length);
  }
  ```

### 5. Function Types

You can define types for entire functions, including parameter and return types:

```typescript
let myFunc: (a: number, b: number) => number;

myFunc = function (x: number, y: number): number {
  return x + y;
};
```

### 6. Type Aliases

Type aliases allow you to give a name to a type, which can be useful for simplifying complex types.

- Alias for primitive types:

  ```typescript
  type StringOrNumber = string | number;
  let id: StringOrNumber = 123;
  ```

- Alias for function types:

  ```typescript
  type MathFunction = (x: number, y: number) => number;
  let add: MathFunction = (a, b) => a + b;
  ```

### 7. Interfaces

Interfaces are used to define object structures. They allow you to define the shape of an object.

- Basic Interface Example:

  ```typescript
  interface Person {
    name: string;
    age: number;
    greet(): string;
  }

  let person: Person = {
    name: "Suryansh",
    age: 25,
    greet() {
      return `Hello, my name is ${this.name}.`;
    },
  };
  ```

## Test Sheet - Day 2

### Multiple Choice

1. What type is used for functions that do not return a value?

   - any
   - **void**
   - never

2. How do you specify that a parameter is optional in TypeScript?
   - **With `?` after the parameter name**
   - With `*` after the parameter name
   - By default, all parameters are optional in TypeScript

### Short Answer

1. Write a TypeScript function `multiply` that accepts two parameters `a` and `b`, both as `number`, and returns the product of the two numbers.
   ```typescript
   function multiply(a: number, b: number): number {
     return a * b;
   }
   ```
2. What is the difference between `void` and `never` types? Provide an example of each.

   ```typescript
   // void - is a type used when a function does not return any type
   function sayHello(): void {
     console.log("Hello !!");
   }

   // never - is a type used when a function never returns a value
   function throwInvalidNameError(): never {
     throw new Error("Invalid name!");
   }
   ```

### Coding Challenge

Write a TypeScript interface called Car that includes properties for `make`, `model`, and `year` (all as `string`), and a method `startEngine` that returns a `string`. Then create an object of type `Car` and call its `startEngine` method.

```typescript
// solution

interface Car {
  make: string;
  model: string;
  year: string;
  startEngine(): string;
}

let car1: Car = {
  make: "Tesla",
  model: "Model S",
  year: "2023",
  startEngine: () => "Engine started!",
};

let output = car1.startEngine();
console.log(output);
```

## Day 3: Classes, Access Modifiers, and Inheritance

### 1. Classes in TypeScript

A class in TypeScript is similar to a class in object-oriented programming languages like Java or C#. TypeScript allows you to define a blueprint for creating objects with properties and methods.

- Basic Class Syntax:

  ```typescript
  class Person {
    name: string;
    age: number;

    constructor(name: string, age: number) {
      this.name = name;
      this.age = age;
    }

    greet(): string {
      return `Hello, my name is ${this.name}`;
    }
  }

  const person1 = new Person("Suryansh", 25);
  console.log(person1.greet());
  ```

### 2. Access Modifiers

TypeScript provides three access modifiers:

- **public**: Accessible everywhere (default if no modifier is specified).

- **private**: Only accessible within the class.

- **protected**: Accessible within the class and subclasses.

- **Example with Access Modifiers**:

```typescript
class Animal {
  public name: string;
  private age: number;
  protected type: string;

  constructor(name: string, age: number, type: string) {
    this.name = name;
    this.age = age;
    this.type = type;
  }

  public getAnimalInfo(): string {
    return `${this.name} is a ${this.type}.`;
  }

  private getAge(): number {
    return this.age;
  }
}

const dog = new Animal("Dog", 5, "Mammal");
console.log(dog.getAnimalInfo()); // Accessible
// dog.age // Error: 'age' is private
```

### 3. Inheritance in TypeScript

Inheritance allows a class to derive properties and methods from another class. In TypeScript, inheritance is implemented using the `extends` keyword.

- **Example of Inheritance**:

  ```typescript
  class Animal {
    name: string;

    constructor(name: string) {
      this.name = name;
    }

    move(distance: number): string {
      return `${this.name} moved ${distance} meters.`;
    }
  }

  class Bird extends Animal {
    fly(): string {
      return `${this.name} is flying.`;
    }
  }

  const bird = new Bird("Parrot");
  console.log(bird.move(10)); // Parrot moved 10 meters.
  console.log(bird.fly()); // Parrot is flying.
  ```

### 4. Readonly Properties

The readonly modifier ensures that a property cannot be changed after it is initialized.

- **Example**:

  ```typescript
  class Car {
    readonly make: string;
    model: string;

    constructor(make: string, model: string) {
      this.make = make;
      this.model = model;
    }

    displayInfo(): string {
      return `This is a ${this.make} ${this.model}.`;
    }
  }

  const car = new Car("Tesla", "Model S");
  console.log(car.displayInfo());
  // car.make = "Ford"; // Error: Cannot assign to 'make' because it is a read-only property.
  ```

### 5. Getters and Setters

Getters and setters allow you to control access to the properties of a class while allowing for validation logic.

- **Example**:

  ```typescript
  class Person {
    private _age: number;

    constructor(age: number) {
      this._age = age;
    }

    get age(): number {
      return this._age;
    }

    set age(newAge: number) {
      if (newAge > 0) {
        this._age = newAge;
      } else {
        console.log("Age must be a positive value.");
      }
    }
  }

  const person = new Person(25);
  console.log(person.age); // 25
  person.age = 30; // setter is called
  console.log(person.age); // 30
  ```

## Test Sheet - Day 3

### Multiple Choice

1. Which access modifier allows access to a property or method from within the class and its subclasses, but not from outside?

   - public
   - private
   - **protected**

2. What is the purpose of the `readonly` modifier in TypeScript?
   - To allow properties to be read and written
   - To allow properties to be read but not modified
   - **To allow properties to be modified only once**

### Short Answer

1. Write a TypeScript class `Employee` with `name` as a public property, `salary` as a private property, and a method `getSalary()` that returns the salary.

   ```typescript
   class Employee {
     public name: string;
     private salary: number;

     constructor(name: string, salary: number) {
       this.name = name;
       this.salary = salary;
     }

     getSalary(): number {
       return this.salary;
     }
   }
   ```

2. What is the difference between the `private` and `protected` access modifiers?

   ```typescript
   // private - means member will not be accessible outside class
   // protected - means member will be only by the class and its subclass

   // <!-- Example -->
   class Person {
     protected name: string;
     private gender: string;

     constructor(name: string, gender: string) {
       this.name = name;
       this.gender = gender;
     }

     // gender is easily accessible inside Person class
     public getGender() {
       return this.gender;
     }
   }

   class Employee extends Person {
     // name is accessible inside Employee class
     // but gender is not because gender is private member of
     // Person class and can be accessed inside that class only
     public getName() {
       return this.name;
     }
   }

   let emp1 = new Employee("Suryansh", "M");
   console.log(emp1.getName());
   ```

### Coding Challenge

Create a class called Book with the following:

A readonly property title of type string.
A protected property author of type string.
A public method getAuthor() that returns the author.
Extend this class into a subclass called Ebook with an additional public method readBook() that logs the title and author.

```typescript
// solution

class Book {
  readonly title: string;
  protected author: string;

  constructor(title: string, author: string) {
    this.title = title;
    this.author = author;
  }

  public getAuthor() {
    return this.author;
  }
}

class EBook extends Book {
  public readBook() {
    console.log(`The author of ${this.title} book is ${this.author}.`);
  }
}
```

## Day 4: Advanced Types & Type Manipulation

### 1. Type Aliases and Interfaces

**Type Aliases**:

- A Type Alias defines a type with a custom name.
- It is useful for complex type definitions or for reusing types.

```typescript
type ID = string | number;

type User = {
  name: string;
  age: number;
};
```

**Interfaces**:

- Interfaces are mainly used for object types. They define the shape of an object.
- You can extend interfaces but not type aliases.

```typescript
interface Person {
  name: string;
  age: number;
}

// Extending an interface
interface Employee extends Person {
  position: string;
}
```

**When to Use Each**:

- **Use interfaces** when you are defining object shapes and prefer extending them in a more object-oriented way.
- **Use type aliases** for defining unions, intersections, and complex types that aren't just objects.

### 2. Intersection Types

- Intersection types allow you to combine multiple types into one.

```typescript
type Admin = {
  adminPrivileges: string[];
};

type Employee = {
  name: string;
  age: number;
};

type AdminEmployee = Admin & Employee;

let adminEmployee: AdminEmployee = {
  name: "Alice",
  age: 30,
  adminPrivileges: ["manage-system", "delete-records"],
};
```

### 3. Mapped Types

- Mapped types allow you to create new types by transforming existing types.
- `Partial<T>`: Makes all properties of `T` optional.

  ```typescript
  interface Product {
    id: number;
    name: string;
    price: number;
  }

  type PartialProduct = Partial<Product>; // All fields optional
  ```

- `Readonly<T>`: Makes all properties of `T` read-only.

  ```typescript
  type ReadonlyProduct = Readonly<Product>; // All fields are readonly
  ```

### 4. Utility Types

- `Pick<T, K>`: Selects a subset of properties from type `T`.

  ```typescript
  type ProductNameAndPrice = Pick<Product, "name" | "price">;
  ```

- `Omit<T, K>`: Omits a subset of properties from type `T`.

  ```typescript
  type ProductWithoutID = Omit<Product, "id">;
  ```

- `Record<K, T>`: Creates an object type with keys `K` and values `T`.
  ```typescript
  type UserRoles = "admin" | "user";
  type UserPermissions = Record<UserRoles, string[]>; // Record<"admin" | "user", string[]>
  ```

### 5. Conditional Types

Conditional types allow you to choose a type based on a condition.

```typescript
type IsString<T> = T extends string ? "Yes" : "No";

type Test1 = IsString<string>; // "Yes"
type Test2 = IsString<number>; // "No"
```

### 6. Type Narrowing

- Type narrowing is when TypeScript automatically narrows down the type based on conditions (type guards).

```typescript
function printValue(val: string | number) {
  if (typeof val === "string") {
    console.log(`String: ${val}`);
  } else {
    console.log(`Number: ${val}`);
  }
}
```

- **Type Guards**: Use `typeof`, `instanceof`, or custom type predicates to refine the type within a block of code.

## Test Sheet - Day 4

### Multiple Choice

1. Which of the following is a utility type that makes all properties of an object type optional?

   - Readonly
   - **Partial**
   - Omit

2. What is an intersection type in TypeScript?

   - A type that includes only common properties of two types
   - **A type that combines multiple types into one**
   - A type that makes all properties readonly

### Short Answer

1. What is the difference between a type alias and an interface? Provide examples for both.

   ```typescript
   // Type alias - it is a type definition for a complex type created using multiple types. For ex -
   type StringOrBoolean = string | boolean;
   let isPublic: StringOrBoolean = "true";

   // Interface - It is also a type definition used for objects. An interface can be extended. For ex -
   interface Employee {
     id: number;
     name: string;
     salary: number;
   }

   interface Admin extends Employee {
     adminPrivalges: string[];
   }
   ```

2. What is type narrowing? Write an example function that narrows down a union type (number | string) based on a condition.

   ```typescript
   // Type narrowing is cutting down the types from a list of types based on conditional checks placed or type guards like typeof, instanceof. For ex -
   function narrowType(salary: number | string) {
     if (typeof salary === "number") {
       console.log(`Number - ${salary}`);
     } else if (typeof salary === "string") {
       console.log(`String - ${salary}`);
     }
   }
   ```

### Coding Challenge

Create a TypeScript type alias Person with properties name and age, and a second type alias Employee that includes Person and an additional property position. Then create an object of type Employee.
Write a function getUserInfo that takes a parameter of type Person | Employee and prints different messages depending on whether the person is an employee or not. Use type narrowing to check if the parameter is an employee.

```typescript
// solution
type Person = {
  name: string;
  age: number;
};

type Employee = Person & {
  position: string;
};

let employee: Employee = {
  name: "John",
  age: 30,
  position: "Manager",
};

function getUserInfo(user: Person | Employee) {
  if ("position" in user) {
    console.log(`${user.name} is an Employee with position ${user.position}.`);
  } else {
    console.log(`${user.name} is not an Employee.`);
  }
}

getUserInfo(employee);
// Output: "John is an Employee with position Manager."
```

## Day 5: Advanced Functions, Generic Types, and Utility Types

### 1. Generic Functions and Constraints Recap

Generics allow you to create flexible, reusable functions and classes that work with multiple types, while maintaining type safety. You can also add constraints to ensure the generic type meets specific conditions.

**Why Use Generics?**

Without generics, you’d need to define a separate version of a function for every type you want it to work with, or you’d have to use the any type, which would remove type safety.

For example, without generics:

```typescript
function identity(arg: any): any {
  return arg;
}
```

Using any doesn’t preserve the type information. If you pass a string, the return type is any, not specifically a string, which can lead to bugs and less readability.

**Generic Syntax**

Generics are introduced using angle brackets (<>) and allow the type to be a parameter.

```typescript
function identity<T>(arg: T): T {
  return arg;
}
```

In this function:

- `T` is a generic type parameter.
- The parameter `arg` has the type `T`, and the function returns a value of type `T`.

This ensures that if you call the function with a string, the return type will be a string. If you call it with a number, the return type will be a number.

**Example of Using Generics**

```typescript
function identity<T>(arg: T): T {
  return arg;
}

let result1 = identity<string>("Hello World"); // T is string, return type is string
let result2 = identity<number>(100); // T is number, return type is number
```

Here, TypeScript infers the type you provide. The identity function adapts to the type T based on the type you pass as an argument.

**Type Inference with Generics**

Often, TypeScript can infer the type without explicitly specifying it:

```typescript
let result = identity("Hello!"); // T is inferred as string
```

TypeScript infers `T` from the argument `"Hello!"`, so you don’t need to specify the type manually.

**Generic Constraints**

You can restrict the type parameter to specific types or interfaces using constraints. For example, if you want to ensure that a type has certain properties, you can use the `extends` keyword:

```typescript
function loggingLength<T extends { length: number }>(arg: T): number {
  return arg.length;
}
```

Here, `T` is constrained to types that have a `length` property (like arrays, strings, etc.).

Examples:

```typescript
loggingLength("Hello World"); // Works, because string has a length
loggingLength([1, 2, 3, 4]); // Works, because array has a length
loggingLength(10); // Error, because number doesn't have a length
```

**Working with Multiple Type Parameters**

You can define functions with multiple generic type parameters:

```typescript
Copy code
function merge<T, U>(obj1: T, obj2: U): T & U {
return { ...obj1, ...obj2 };
}

const person = merge({ name: "Suryansh" }, { age: 25 });
console.log(person); // Output: { name: 'Suryansh', age: 25 }
```

Here, `merge` combines two objects into one. The types `T` and `U` represent the types of the two objects being merged, and the return type is the intersection of both types (`T & U`).

**Generic Interfaces**

Interfaces can also be generic:

```typescript
interface Box<T> {
  contents: T;
}

let box: Box<string> = { contents: "A gift" };
console.log(box.contents); // Output: "A gift"
```

Here, the `Box` interface has a generic type `T`, and when we use the interface, we specify that `T` should be a `string`. This makes the `contents` property a `string`.

**Generic Classes**

Classes can also be generic in TypeScript. Here’s an example of a generic class:

```typescript
class Box<T> {
  contents: T;

  constructor(value: T) {
    this.contents = value;
  }

  getContents(): T {
    return this.contents;
  }
}

let stringBox = new Box<string>("Generics are fun!");
let numberBox = new Box<number>(100);

console.log(stringBox.getContents()); // Output: "Generics are fun!"
console.log(numberBox.getContents()); // Output: 100
```

**Bounded Generics with Interfaces**

If you want to limit the types that can be passed to a generic function, you can use interfaces:

```typescript
interface HasName {
  name: string;
}

function greet<T extends HasName>(obj: T): void {
  console.log("Hello, " + obj.name);
}

greet({ name: "Suryansh", age: 25 }); // Valid, as the object has a name property
greet({ age: 25 }); // Error, as the object does not have a name property
```

In this case, we’ve constrained `T` to types that have a `name` property. This allows the `greet` function to be type-safe when working with objects that meet this interface.

**Conclusion**

Generics provide a powerful way to create flexible and reusable code while maintaining type safety in TypeScript. They enable you to write functions, classes, or interfaces that can handle various types without compromising type information or safety.

**Key Benefits of Generics**

- Reusability: You write the logic once but can use it for many types.
- Type Safety: Unlike any, generics maintain type information.
- Flexibility: Generics work with multiple types, allowing flexibility without losing the structure of your code.-

## 2. Utility Types: Advanced

Beyond `Partial`, `Pick`, and `Omit`, TypeScript provides several other useful utility types. Let’s cover some important ones:

1. `Exclude<Type, ExcludedUnion>`

   Constructs a type by excluding certain types from a union.

   ```typescript
   type Primitive = string | number | boolean;
   type NonBoolean = Exclude<Primitive, boolean>; // string | number
   ```

2. `Extract<Type, Union>`

   Extracts types that are assignable to a union.

   ```typescript
   type Primitive = string | number | boolean;
   type OnlyString = Extract<Primitive, string>; // string
   ```

3. `NonNullable<Type>`

   Removes null and undefined from a type.

   ```typescript
   type MaybeNumber = number | null | undefined;
   type DefiniteNumber = NonNullable<MaybeNumber>; // number
   ```

4. `ReturnType<Type>`

   Infers the return type of a function.

   ```typescript
   function getUserAge(): number {
     return 25;
   }

   type AgeType = ReturnType<typeof getUserAge>; // number
   ```

5. `InstanceType<Type>`

   Constructs a type representing the instance type of a constructor function or class.

   ```typescript
   class User {
     constructor(public name: string, public age: number) {}
   }

   type UserInstance = InstanceType<typeof User>; // User
   ```

6. `ThisType<Type>`

   Used for "this"-related typing, especially useful in object-oriented patterns.

   ```typescript
   interface Obj {
     name: string;
     greet(): void;
   }

   const myObj: ThisType<Obj> = {
     name: "Suryansh",
     greet() {
       console.log(`Hello, ${this.name}!`);
     },
   };

   myObj.greet(); // "Hello, Suryansh!"
   ```

### 3. Conditional Types

Conditional types in TypeScript provide a way to define types that depend on a condition, making your types more dynamic and flexible. They allow you to create types that change based on whether a certain condition is met or not, similar to how conditional logic works in functions.

The syntax for conditional types looks like this:

```typescript
T extends U ? X : Y
```

- If T extends U, the type resolves to X.
- Otherwise, the type resolves to Y.

This means that you can apply a condition to types and decide which type should be assigned based on whether the condition is true or false.

**Basic Example of Conditional Types**
Here’s a simple example of how conditional types work:

```typescript
type IsString<T> = T extends string
  ? "Yes, it's a string"
  : "No, it's not a string";

type A = IsString<string>; // A is "Yes, it's a string"
type B = IsString<number>; // B is "No, it's not a string"
```

In this example:

- `IsString<T>` checks if `T` extends the type `string`.
- If `T` is a `string`, it resolves to `"Yes, it's a string"`.
- If `T` is not a `string`, it resolves to `"No, it's not a string"`.

**How Conditional Types Work**

The `extends` keyword is used to check whether a type satisfies a condition. This is similar to how you would check if a class extends another class or if an interface extends another interface. With conditional types, you're checking if a type satisfies certain constraints.

**Real-world Use Cases of Conditional Types**

1. **Extracting Types Based on Conditions**

   You can use conditional types to extract certain types based on conditions. For example, you might want to extract the return type of a function or ensure a function always returns a certain type.

   ```typescript
   type GetReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

   function add(a: number, b: number): number {
     return a + b;
   }

   type ReturnTypeOfAdd = GetReturnType<typeof add>; // ReturnTypeOfAdd is number
   ```

   In this example:

   - `T` extends `(...args: any[]) => infer R` checks if `T` is a function.
   - If it is, it uses the `infer` keyword to extract the return type `R` of the function.
   - Otherwise, it resolves to `never`.

2. **Filtering Types**

   Conditional types are useful when you want to filter out certain types from a union type:

   ```typescript
   type ExcludeString<T> = T extends string ? never : T;

   type Result = ExcludeString<string | number | boolean>; // Result is number | boolean
   ```

In this example:

- `ExcludeString<T>` checks if `T` is `string`.
- If `T` is `string`, it resolves to `never` (which effectively removes it from the union).
- Otherwise, it keeps the type.

3. Mapping Over Unions

   Conditional types can also iterate over union types and apply transformations:

```typescript
type WrappedInArray<T> = T extends any ? T[] : never;

type Result = WrappedInArray<string | number>; // Result is string[] | number[]
```

In this example:

- `WrappedInArray<T>` checks if `T` is part of a union and wraps each type in an array.
- The result is `string[] | number[]` because `string` and `number` are the two types in the union, and each is wrapped in an array.

**Advanced Concepts: Infer Keyword**

One of the most powerful features of conditional types is the `infer` keyword, which allows you to infer or "capture" a type from some part of the condition.

For example, you can use `infer` to extract return types from function signatures:

```typescript
type GetReturnType<T> = T extends (...args: any[]) => infer R ? R : never;

function greet(): string {
  return "Hello, world!";
}

type GreetReturnType = GetReturnType<typeof greet>; // GreetReturnType is string
```

Here, the `infer` keyword captures the return type of the function and assigns it to `R`, which you can then use in the conditional type.

**Practical Use Cases of Conditional Types**

1. **Creating Utility Types**

Many of TypeScript's built-in utility types (like `ReturnType`, `Exclude`, `Extract`, etc.) are based on conditional types.

- `ReturnType` extracts the return type of a function.
- `Exclude` removes certain types from a union.
- `Extract` keeps only certain types from a union.

**Example of `ReturnType`**:

```typescript
type ReturnType<T> = T extends (...args: any[]) => infer R ? R : any;

function multiply(a: number, b: number): number {
  return a \* b;
}

type MultiplyReturnType = ReturnType<typeof multiply>; // number
```

2. **Building Custom Utility Types**

You can create your own utility types using conditional types. For instance, a utility type to check if a type is an array:

```typescript
type IsArray<T> = T extends any[] ? true : false;

type A = IsArray<number[]>; // true
type B = IsArray<string>; // false
```

**Distributive Conditional Types**

Conditional types can distribute over union types automatically. This is known as a distributive conditional type. It means the conditional type is applied individually to each member of the union.

```typescript
type Distribute<T> = T extends any ? T[] : never;

type DistributedUnion = Distribute<number | string>; // number[] | string[]
```

Here, `number | string` is a union type, and the conditional type applies to both `number` and `string` separately. The result is `number[] | string[]`.

**Combining Conditional Types with Utility Types**

You can combine conditional types with TypeScript’s utility types to create powerful abstractions. Here’s an example that removes all `readonly` modifiers from an object type:

```typescript
type Mutable<T> = {
  -readonly [P in keyof T]: T[P];
};

interface User {
  readonly id: number;
  readonly name: string;
}

type MutableUser = Mutable<User>; // { id: number; name: string }
```

**Example: Recursive Conditional Types**

Conditional types can even be recursive. For instance, if you want to flatten a nested array type:

```typescript
type Flatten<T> = T extends any[] ? Flatten<T[number]> : T;

type A = Flatten<number[][][]>; // number
```

Here, `Flatten<T>` checks if `T` is an array (`T extends any[]`), and if so, it recursively flattens it by accessing `T[number]`, which gives the type of the elements of the array. This process continues until the type is no longer an array, resulting in a flattened type.

**Summary of Conditional Types**

- **Type Resolution**: Conditional types resolve to different types based on a condition.
- **Syntax**: `T extends U ? X : Y` – If `T` extends `U`, the type resolves to `X`, otherwise to `Y`.
- **Type Inference**: You can infer types dynamically using the `infer` keyword.
- **Distributive**: Conditional types distribute over union types automatically.
- **Utility Types**: Many TypeScript utility types like `ReturnType`, `Exclude`, and `Extract` are built using conditional types.

Conditional types allow you to create flexible, reusable types that adapt based on the input, helping you enforce type safety while still accommodating various use cases in complex type systems.

### 4. Function Overloads

You can define multiple function signatures to handle different input types and behaviors.

```typescript
function combine(a: number, b: number): number;
function combine(a: string, b: string): string;
function combine(a: any, b: any): any {
  return a + b;
}

combine(1, 2); // 3
combine("a", "b"); // "ab"
```

## Test Sheet 1 - Day 5

### Multiple Choice

1. What does the Extract utility type do?

   - **Extracts types assignable to a union**
   - Excludes certain types from a union
   - Removes null and undefined from a type

2. How can you infer the return type of a function in TypeScript?

   - **Using the ReturnType utility type**
   - Using the InstanceType utility type
   - Using the Exclude utility type

### Short Answer

1. What does the NonNullable utility type do? Write an example.

   ```typescript
   // NonNullable utility type removes null and undefined types from a union of types. For ex -
   type MayBeString = string | null | undefined;
   type NonNullString = NonNullable<MayBeString>; // string
   ```

2. Write a TypeScript function sumOrConcat that either adds two numbers or concatenates two strings, depending on the types of the inputs. Demonstrate function overloads.

   ```typescript
   function sumOrConcat(a: number, b: number): number;
   function sumOrConcat(a: string, b: string): string;
   function sumOrConcat(a: any, b: any): any {
     return a + b;
   }

   console.log(sumOrConcat(3, 4)); // 7
   console.log(sumOrConcat("Hello ", "Suryansh!")); // "Hello Suryansh!"
   ```

### Coding Challenge

Create a TypeScript class Queue that uses generics. It should have methods for enqueue (adding an item), dequeue (removing an item), and peek (checking the first item in the queue). Use constraints to ensure that the queue only works with types that have a toString() method.

```typescript
// solution
class Queue<T> {
  private data: T[] = [];

  enqueue(element: T) {
    this.data.push(element);
  }

  dequeue(): T | undefined {
    return this.data.shift();
  }

  peek(): T | undefined {
    return data[0];
  }
}

let stringQueue = new Queue<string>();
stringQueue.enqueue("first");
stringQueue.enqueue("second");
console.log(stringQueue.peek()); // "first"
stringQueue.dequeue();
console.log(stringQueue.peek()); // "second"
```

## Test Sheet 2 - Day 5

### Multiple Choice

1. Which utility type is used to combine two types into one that contains only the properties common to both?

   - Union
   - **Intersection**
   - Exclude

2. What does the `ReturnType<T>` utility type do?

   - Converts the type `T` into a string
   - **Extracts the return type of a function type `T`**
   - Extracts the instance type of a class

### Short Answer

1. What is the `Exclude<T, U>` utility type used for? Write an example of using `Exclude` to remove certain types from a union.

   ```typescript
   // Exclude<T, U> - It is used to exclude type T from union U

   type Primitive = string | number | boolean;
   type NonBooleanPrimitive = Exclude<Primitive, boolean>; // string | number
   ```

2. Write a TypeScript function `addOrMerge` that can either add two numbers or merge two arrays. Demonstrate function overloads.

   ```typescript
   function addOrMerge(a: number, b: number): number;
   function addOrMerge<T>(a: T[], b: T[]): T[];
   function addOrMerge<T>(a: T, b: T): T {
     if (Array.isArray(a) && Array.isArray(b)) {
       return a.concat(b);
     }
     return a + b;
   }

   console.log(addOrMerge(3, 4)); // 7
   console.log(addOrMerge([3], [4])); // [3, 4]
   ```

### Coding Challenge

Create a generic class called Stack that implements the following methods:

- **push(item: T)** - Adds an item to the stack.
- **pop()** - Removes and returns the last item.
- **peek()** - Returns the last item without removing it.

Ensure that the `Stack` class only works with types that have a `toString()` method.

```typescript
// solution
interface HasToString {
  toString: () => string;
}

class Stack<T extends HasToString> {
  private data: T[] = [];

  push(item: T): void {
    this.data.push(item);
  }

  pop(): T | undefined {
    return this.data.pop();
  }

  peek(): T | undefined {
    const length = this.data.length;
    if (length === 0) return undefined;
    return this.data[length - 1];
  }
}

class Person implements HasToString {
  constructor(private name: string) {}

  toString(): string {
    return this.name;
  }
}

let personStack = new Stack<Person>();
personStack.push(new Person("Alice"));
personStack.push(new Person("Bob"));
console.log(personStack.peek()?.toString()); // Bob
personStack.pop();
console.log(personStack.peek()?.toString()); // Alice
```

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
let isPublic: StringOrBoolean = 'true';

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
  if(typeof salary === 'number') {
    console.log(`Number - ${salary}`)
  } else if (typeof salary === 'string') {
    console.log(`String - ${salary}`)
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
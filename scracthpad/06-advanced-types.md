Section 06: Namespaces and Modules
==================================
It is time to moving forward and review the advanced features that TypeScript offers on Types. The next image summarized the contents of this section:

![Advanced Types](../assets/s06-advanced-types.png "Advanced Types")


Index
-----------------------------
1. Intersection Types
2. More on Type Guards
3. Discriminated Unions
4. Type Casting
5. Index Properties
6. Function Overloads
7. Optional Chaining
8. Nullish Coalescing
9. Wrap Up
10. Resources

Intersection Types
-----------------------------
Intersection types allow us to combine our types. Please check the snippet below:

```typescript
type Admin = {
    name: string;
    privelges: string[];
}

type Employee = {
    name: string;
    startDate: Date;
}

type ElevatedEmployee = Admin & Employee;

const employee: ElevatedEmployee = {
    name: 'Edward',
    privelges: ['alchemy'],
    startDate: new Date(),
}
```

Notice that the `ElevatedEmployee` is the combined type of `Admin` and `Employee`, and the key operator for intersect type is the ampersand `&`. With this definition, we can create an object with the combined type as is `employee`. We could get the same result using interfaces, as shown next:

```typescript
interface Admin {
    name: string;
    privelges: string[];
}

interface Employee = {
    name: string;
    startDate: Date;
}

interface ElevatedEmployee extends Admin, Employee {};

const employee: ElevatedEmployee = {
    name: 'Edward',
    privelges: ['alchemy'],
    startDate: new Date(),
}
```

However, this syntax is a little bit longer, and it is common use the `type` version. So, for object types, intersection types it is simply the combination of these object properties. This features can sometimes be useful. You will not use the all the time but you definitely can encounter situations where you can express something in a simpler way by using intersection types.

More on Type Guards
-----------------------------
Discriminated Unions
-----------------------------
Type Casting
-----------------------------
Index Properties
-----------------------------
Function Overloads
-----------------------------
Optional Chaining
-----------------------------
Nullish Coalescing
-----------------------------
Wrap Up
-----------------------------
Resources
-----------------------------

Intro to namespace
-----------------------------
1. Check the next code:

```javascript

namespace myMath() {
	const PI = 3.14;

	export function calculateCircumference(diameter: number) {
		return diameter * PI;
	}

	export function calculateRectangle(width: number, length:number) {
		return width * length;
	}
}

```

2. The namespace allow us split our code avoiding the use of global scope. The TS compiler use JS IIFE to split the code blocks


Namespaces and Multiple Files
-----------------------------
1. We can split our `myMath` namespace in two files `circleMath.ts` and `rectangleMath.ts`, and add the respective calculate functions.
2. If we run the new structure the browser will throw the error `Uncaught Reference`. To solve this issue we have three possibilities:
    1. Import the  `circleMath.js` and the `rectangleMath.js` files in the `index.html`
    2. Use the TypeScript option compiler `-- outFile {{outputsFile.js}} {{inputFile*.ts}}`
    3. Please check the Namespace Import section

Namespace Imports
-----------------
1. TypeScript has his own syntax to import namespace. The next code shows this syntax:

```javascript

/// <reference path="circleMath.ts />"
/// <reference path="rectangleMath.ts />"

```

More on Namespaces
------------------
1. Nested Namespaces
2. Set namespace aliases

Limitations Namespaces
----------------------
1. Namespaces are not declarative.
2. For small projects use Namespaces. For big projects use Modules.

Modules
-------
1. For use modules, you should change your project structure to something like:

```
app
|-- modules
|   |-- moduleFileOne.ts
|   |-- moduleFileTwo.ts
|-- app.ts
```

2. In the app.ts you will `import` the element that are `export` in the modules files.

Loading Modules
---------------
1. The module dependency management in JavaScript has a long history. Please check the article [JavaScript Module System Shutdown](https://auth0.com/blog/javascript-module-systems-showdown/)
2. For this learning you will use the *All-in-one solution: SystemJS*
    1. Install it with `npm install --save systemjs`
    2. Add the respective configuration in the `index.html` file

Importing and Exporting Modules
-------------------------------
1. Bear in mind that first you have to export and then you import. Then follow the next syntax:

```javascript
// rectangle.ts file
export function calculateRectangle(width: number, length:number) {
	return width * length;
}

```

```javascript
// app.ts file
import {calculateRectangle} from 'path/to/rectangle.ts'

console.log(calculateRectangle(20,10))
```

2. Alias are enable in module imports

```javascript
// app.ts file
import * as Rectangle from 'path/to/rectangle.ts'
console.log(Rectangle.calculateRectangle(20,10))

```

3. Export default syntax

```javascript
// rectangle.ts file
export default function calculateRectangle(width: number, length:number) {
	return width * length;
}

```

```javascript
// app.ts file
import calcRectangle from 'path/to/rectangle.ts'

console.log(calcRectangle(20,10))
```

Module Resolution
-----------------
1. Import with relative paths
2. Import with absolute paths. Common use whe you use TypeScript with Angular
3. Automatic resolution of `.ts` files

Namespaces vs Modules
---------------------

Namespaces
- Organize application with JavaScript Objects
- Can be split up over multiple files
- No module loader required
- Dependencies get difficult to manage in bigger applications

Modules
- Organize application with real Modules
- Can be split up over multiple files
- Module loader required
- Explicit dependency declaration
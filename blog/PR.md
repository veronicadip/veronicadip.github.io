# My experience making a pull request to an open source project

While making my first pull request to a real project, I had to learn a lot, from setting up the project to new concepts of JavaScript and TypeScript.

## JavaScript functions can be used like React classes

We know that in JavaScript, classes don't exist, but I didn't know that functions have a lot in commmon with them. At the end, the computer compiles the class from React as a JavaScript function.

The fact that surprised me the most, is that you can make a `new` instance of a function, passing it values for it to use.

In conclusion, is the same doing this:

```js
class Person {
        constructor(name) {
                this.name = name
        }
        greeting() {
                console.log(`Hi! my name is ${name}`)
        }
};

const John = new Person("John")
```

And doing this:

```js
const Person = function(name) {
        const greeting = function() {
                console.log(`Hi! my name is ${name}`)
        }
        return {
                name: name,
                greeting: greeting
        }
};

const John = new Person("name")
```

## Make declarations in TypeScript using .d.ts

My contribution was migrating some JavaScript files to TypeScript, so at one point I needed to make a type declaration of functions of a library. To do that, I needed to create a `.d.ts` file.

These files contain only type information (for typechecking), this means that these don't produce any `.js` outputs.

## Usually node_modules folders are git ignored

The folder `node_modules` is created by `npm` or `yarn` and it contains all the packages installed locally from `packages.json`. 

This folder is usually set to be ignored by git, so, if you need to add a `d.ts` for another file that is in `node_modules`, you'll need to put that new file in a directory that isn't affected by `.gitignore` (because you'll want to commit that change).

## You can convert any value to the corresponding boolean primitive

You can convert any value to a Boolean primitive one using the `Boolean()` constructor. This is specially useful when you need a function to return a strictly boolean value but it returns `truthy` or `falsy`.

You can use it like this:

```js
Boolean("Your value");
```

You can do the same using the double NOT (`!!`):

```js
!!"Your value"
```

## Indicating React that your prop isn't undefined

When you are passing a prop that might be undefined but you are sure that it have a value, you can add an exclamation symbol (!) at the end:

```js
const myFunction = function(myProp) {
        return (
                <div>
                <MyComponent neededProp={myProp!} />
                </div>
        )
}
```

## Conclusion

I've learned a lot by just making one pull request, from reading someone else's code to new concepts of languages that I was used to use alone.

My conclusion is that, when you feel that you aren't learning so much from your solo projects, this is a great way to learn and practice new concepts.
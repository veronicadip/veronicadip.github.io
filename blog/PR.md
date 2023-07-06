# My experience making a pull request to an open source project

## JavaScript functions can be used like React classes

const Dog = function(name) {
console.log("function called")

        const barf = function() {
                console.log(`bafg! I'm ${name}`)
        }

        return {
                name: name,
                barf: barf,
        }

}

// returns object with keys name and barf with its respective values

class Dog {
initialize(name) {
this.name = name
}

      barf() {

}

const puki = new Dog("puki")
console.log(puki)
console.log(puki.barf())

the class is a sugar code for the js function

## make declarations in ts (file.d.ts)

## while making a declaration, you can only use types

interface is also a type

## usually node_modules folders are git ignored

if you change something about the modules, it needs to be outside that ignored folder

## you can convert something to a boolean value using Boolean("example")

it can also work using !!("example"), the first exclamation to convert the content to boolean, and the second to undo the first "not" (the first one reverts the correct value while converting, the second one makes it return the right boolean value)

## tell ts what's inside an array

interface ObjectsExample {
...
}

const arrayExample: ObjectsExample[] = [
{
...
},
{
...
}
]

## manage modules

declare module "example" {
interface MyObject {
..
}
type MyFunction ...

    export {MyObject, MyFunction}

}

# ts interfaces

interface, type, declare

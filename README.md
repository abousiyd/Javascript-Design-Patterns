# Javascript-Design-Patterns

Design patterns are solutions for typical and recurring problems that we may find when developing an application.

Although our application is unique, it will have common parts with other applications: access to data, creation of objects, operations between systems, etc. Instead of reinventing the wheel, we can solve problems using some pattern, as they are proven and documented solutions. For a crowd of programmers.

## [1] The Module Pattern

Originally, the module design pattern was designed to add encapsulation to the classes of a program. In JavaScript, the pattern of the module is used to emulate the concept of class, so that we can have public and private variables and methods.

This represents a benefit because we avoid contaminating the global scope and we have less risk of having a conflict with the functions or variables defined in other scripts on the page. In this pattern, only one object that represents the public API is returned, keeping everything else private.

This is a clean solution to write all the logic of the application privately and only expose the necessary to other parts of the application in a concise way. It is important to emphasize that in JavaScript there is no explicit form of privacy because unlike other languages, it does not have access modifiers. The variables can not be declared technically as private, however, we use the scope of a function to simulate this concept. Within the module pattern, the variables and methods are only visible within the module thanks to a closure. While the variables or methods defined within the result object are available to all.


Js

(() => {

    const module = (() => {

    const _shuffleLogic = arr => arr.sort(() => Math.random() - 0.5)

    const shuffleArray = arr => _shuffleLogic(arr)

    return { shuffleArray }

    })()

    const extendModule = (module => {

        const _filterFalsy = arr => arr.filter(Boolean)

        module.filterFalsy = arr => _filterFalsy(arr)

        return module

    })(module || {})

    console.log(
        module.shuffleArray(['lorem', 'ipsum', 'dolor', 'sit', 'amet']),
        module.filterFalsy([12, null, [], true, 'Laravel', undefined, {}, 0])
    )

})()



## [2] The Constructor Pattern

In classical object-oriented programming languages, a constructor is a special method used to initialize a newly created object once memory has been allocated for it. In JavaScript, as almost everything is an object, we're most often interested in object constructors.

Object constructors are used to create specific types of objects - both preparing the object for use and accepting arguments which a constructor can use to set the values of member properties and methods when the object is first created.

#### There are then four ways in which keys and values can then be assigned to an object:

 Js

(() => {

    // The three common ways to create new objects in JavaScript are as follows:

        const post = {} // || Object.create( Object.prototype ) || new Object()

    // 1 Dot syntax

        post.title = 'My post'

    // 2 Square bracket syntax

        post['text'] = 'Lorem ipsum dolor set...'

    // 3 Object.defineProperty

        const person = {}

        Object.defineProperty(person, 'name', {
            set(value) {
                this._name = value
            },

            get() {
                return this._name.toUpperCase()
            }
        })

        person.name = 'Abdou'

        console.log(person.name)

        // or 

        const defineProp = (obj, key, value) => Object.defineProperty(obj, key, {value})

        const user = {}

        defineProp(user, 'name', 'Abdou')
        defineProp(user, 'surname', 'Bousiyd')

        console.log(user)

    // 4 Object.defineProperties

        const logic = {}

        Object.defineProperties(logic, {
            __userToken__: {
                set(token) {
                    sessionStorage.setItem('__userToken__', token)
                },

                get() {
                    return sessionStorage.getItem('__userToken__')
                }
            },
            __isAuth__: {
                get() {
                    return !!this.__userToken__
                }
            }
        })

})()

    


#### Basic Constructors

By simply prefixing a call to constructor function with the keyword "new", we can tell JavaScript we would like the function to behave like a constructor and instantiate a new object with the members defined by that function.

Inside a constructor, the keyword this references the new object that's being created. Revisiting object creation, a basic constructor may look as follows:



 Js

(() => {

    
    function WtfError(message) {
        if (this instanceof WtfError) {
            this.message = message
        } else return new WtfError(message)
    }

    WtfError.prototype = Object.create(Error.prototype)
    WtfError.prototype.constructor = WtfError
    WtfError.prototype.toString = () => `${this.constructor.name}: ${this.message}`

    // with new

    new WtfError('Custom error message').toString()

    // same as without new

    WtfError('Custom error message').toString()

})()




coming soon ...

## Summary

- Singleton - Share a single global instance throughout our application
- Proxy - Intercept and control interactions to target objects
- Provider - Make data available to multiple child components

## Singleton Pattern

- Singletons are classes which can be instantiated once, and can be accessed globally.
  - True
  - False
- Singleton pattern is used to:
  - For managing global state in an application.
- As there is a possibility to create multiple instances, this does not meet the criteria of singleton pattern

  -

  ```js
  let counter = 0;

  class Counter {
    getInstance() {
      return this;
    }

    getCount() {
      return counter;
    }

    increment() {
      return ++counter;
    }

    decrement() {
      return --counter;
    }
  }

  const counter1 = new Counter();
  const counter2 = new Counter();

  console.log(counter1.getInstance() === counter2.getInstance()); // false
  ```

- Whats the output of code?
-

```js
let instance;
let counter = 0;

class Counter {
  constructor() {
    if (instance) {
      throw new Error('You can only create one instance!');
    }
    instance = this;
  }

  getInstance() {
    return this;
  }

  getCount() {
    return counter;
  }

  increment() {
    return ++counter;
  }

  decrement() {
    return --counter;
  }
}

const counter1 = new Counter();
const counter2 = new Counter();
```

- Error: You can only create one instance!

- Disadvantages:
  - Global behaviour - Understanding the data flow when using a global state can get very tricky as your application grows, and dozens of components rely on each other.
  - Testing - Since we can't create new instances each time, all tests rely on the modification to the global instance of the previous test.

## Proxy Pattern

- A proxy can be useful to add validation. A user shouldn't be able to change person's age to a string value, or give him an empty name. Or if the user is trying to access a property on the object that doesn't exist, we should let the user know.
- JavaScript provides a built-in object called Reflect, which makes it easier for us to manipulate the target object when working with proxies.

```js
const personProxy = new Proxy(person, {
  get: (obj, prop) => {
    console.log(`The value of ${prop} is ${Reflect.get(obj, prop)}`);
  },
  set: (obj, prop, value) => {
    console.log(`Changed ${prop} from ${obj[prop]} to ${value}`);
    Reflect.set(obj, prop, value);
  },
});
```

## Provider pattern

- Advantages of provider pattern:
  - With the Provider pattern, we no longer have to unnecessarily pass props to component that don't care about this data.
  - Prop drilling is solved
- Best Practice - To make sure that components aren't consuming providers that contain unnecessarily values which may update, you can create several providers for each separate usecase.

## Prototype pattern

- The value of **proto** on any instance of the constructor, is a direct reference to the constructor's prototype! Whenever we try to access a property on an object that doesn't exist on the object directly, JavaScript will go down the prototype chain to see if the property is available within the prototype chain.
- Advantages of prototype pattern:
  - The prototype pattern is very powerful when working with objects that should have access to the same properties.
  - The prototype pattern allows us to easily let objects access and inherit properties from other objects.

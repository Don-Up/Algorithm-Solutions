# create an Event Emitter

There is [Event Emitter in Node.js](https://nodejs.org/api/events.html#events_class_eventemitter), Facebook once had [its own implementation](https://github.com/facebookarchive/emitter) but now it is archived.

You are asked to create an Event Emitter Class

```js
const emitter = new Emitter()
```

It should support event subscribing

```js
const sub1  = emitter.subscribe('event1', callback1)
const sub2 = emitter.subscribe('event2', callback2)
// same callback could subscribe 
// on same event multiple times
const sub3 = emitter.subscribe('event1', callback1)
```

`emit(eventName, ...args)` is used to trigger the callbacks, with args relayed

```js
emitter.emit('event1', 1, 2);// callback1 will be called twice
```

Subscription returned by `subscribe()` has a `release()` method that could be used to unsubscribe

```js
sub1.release()
sub3.release()
// now even if we emit 'event1' again, 
// callback1 is not called anymore
```

## Solution Approach

Sure, here is the implementation of an `EventEmitter` class with the described functionality:

```javascript
class EventEmitter {
  constructor() {
    this.events = {};
  }

  subscribe(eventName, callback) {
    if (!this.events[eventName]) {
      this.events[eventName] = [];
    }
    const callbackWrapper = {
      callback,
      release: () => {
        this.events[eventName] = this.events[eventName].filter(cb => cb !== callbackWrapper);
      }
    };
    this.events[eventName].push(callbackWrapper);
    return callbackWrapper;
  }

  emit(eventName, ...args) {
    if (this.events[eventName]) {
      this.events[eventName].forEach(callbackWrapper => {
        callbackWrapper.callback(...args);
      });
    }
  }
}

// Usage Example:

const emitter = new EventEmitter();

const callback1 = (...args) => console.log('callback1', ...args);
const callback2 = (...args) => console.log('callback2', ...args);

const sub1 = emitter.subscribe('event1', callback1);
const sub2 = emitter.subscribe('event2', callback2);
// same callback could subscribe 
// on same event multiple times
const sub3 = emitter.subscribe('event1', callback1);

emitter.emit('event1', 1, 2); // callback1 will be called twice
emitter.emit('event2', 3, 4); // callback2 will be called once

sub1.release();
sub3.release();
// now even if we emit 'event1' again, 
// callback1 is not called anymore
emitter.emit('event1', 5, 6);
```

<audio src="assets/create%20an%20Event%20Emitter.mp3"></audio>

### Explanation:

1. **Constructor**: Initializes an empty object to hold the events.
2. **subscribe(eventName, callback)**:
   - Checks if the event name already exists in the `events` object.
   - If not, initializes it as an empty array.
   - Wraps the callback in an object that includes the `release` method.
   - Adds the wrapped callback object to the array for the event name.
   - Returns the wrapped callback object.
3. **emit(eventName, ...args)**:
   - Checks if the event name exists in the `events` object.
   - If it exists, iterates over the array of wrapped callback objects and calls each callback with the provided arguments.

### Usage Example:
- The provided example shows how to create an `EventEmitter`, subscribe to events, emit events, and release subscriptions.
## Javascript Algorithm

#### we have a palindrome. To reverse a string

> split('').reverse().join('');

```javascript
function reverse (string) {
 var newString = string.split('').reverse().join('');
 return newString;
}
reverse("Hello");/// gives us "olleh"
```

#### What is a Promise?

```
A promise is an object that may produce a single value some time in the future: either a resolved value, or a reason that it’s not resolved (e.g., a network error occurred). A promise may be in one of 3 possible states: fulfilled, rejected, or pending. Promise users can attach callbacks to handle the fulfilled value or the reason for rejection.

#### How Promises Work
A promise is an object which can be returned synchronously from an asynchronous function. It will be in one of 3 possible states:

Fulfilled: **onFulfilled()** will be called (e.g., resolve() was called)
Rejected: **onRejected()** will be called (e.g., reject() was called)
Pending: not yet fulfilled or rejected
```

```javascript
const wait = time => new Promise((resolve) => setTimeout(resolve, time));

wait(3000).then(() => console.log('Hello!')); // 'Hello!'
```

```javascript

```
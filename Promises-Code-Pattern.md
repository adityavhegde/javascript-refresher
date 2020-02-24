Just some mind dump from recent Promises based programming that I did.

I had two Promises - A and B and B depended on some result from A. Eventually both of them return two values X and Y which I need to run the event handler on a UI element. 

I ended up structuring the code like this: 

``` javascript
funct _A() {
  return new Promise((resolve, reject) => { //...if...resolve...else ...reject});
}
```

``` javascript
func _B() {
 // similar to Promise A but dependent on some value that A's resolution has set in the global scope 
}
```

``` javascript
function EvtHandler(e) {
  
  const A = _A();
  
  A
   .then( (resolvedVal) => {
     const B = _B()'
     
      B
       .then(
         // ..some more fetch
       );
    
   })
   .catch();
}
```

After reading the **Async & Performance book**, I think I could have structured this as: 

``` javascript
function EventHandler() {
  A = _A();
  A.then(() => {
  
   return _B(); // this is the same as return new Promise() ... since _B() returns a Promise
  })
  .then((retValOfB) => {
    // ... some more fetch and actual Event Handling code  
  })
  .catch( // catch along any failures );

}
```
This is better than the nesting pattern which I've originally written.

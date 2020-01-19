These are some notes from the you don't know JS series.

It is quite easy for new programmers to confuse the javascript programming language with the runtime that it runs on. With Nodejs not being in pitcure, the only environment that javascript ran on was the browser. With Nodejs, we now have differing sort of dialects of javascripts. Most of the things that appear differing are not within javascript -- it is within the run time.

While running in the browser, some of the functions are provided to javascript developers as API calls. A good example of this is the good old XMLHttpRequest object, which isn't an ECMAscript function, but an API made available via the browser runtime environment. In other words, when such a call is issues, the call is dispatched to the browser which then handles the request.

The difference between runtimes becomes more obvious when we discuss about the DOM. Most DOM functions are made available to javascript via the browser. This means the DOM functions are a set of runtime provided functions. This runtime is refered to as the host environment by Kyle Simpson in his you don't know JS series.

Understanding this key difference between javascript runtime and javascript language is important. It clarifies the discussion regarding the event loop. 

In summary, operations that require interacting with the host environment may be defered to that environment. Such defered operations, on completion examine if the caller provided a callback. On completion the callback is then placed on the event loop. The javascript call stack, when empty will pop an item from the queue's front, put it on the run stack and execute whatever is on the stack.

I am not sure why javascript is refered to as single threaded. What does that really mean -- I am not entirely sure? In a language that offers parallelism via threads, the programmer explicitly writes the threaded aspects of the code. Javascript developers don't have that sort of flexibility. 

**Javascript always executes whatever is on the stack** And often, function callbacks are added to the eventloop asynchronously.

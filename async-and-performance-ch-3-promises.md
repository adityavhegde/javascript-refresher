Promise tasks according to the specification, shouldn't go in the event loop and have their own PromiseJob queue. In the Browser, Promise tasks also get higher priority than the normal event loop tasks.

[Refer the answer here](https://stackoverflow.com/questions/40880416/what-is-the-difference-between-event-loop-queue-and-job-queue)

With Async callbacks' inversion of control, there are these concerns:
1. Calling too early
2. Calling late
3. Never being called 

Promises deal with all of them and establish trust. A Promise will always notify the caller of its resolution. If you register a rejection callback then you will always be notified of that too.

In javascript Async tasks, you cannot rely on which order the callbacks in event loop may execute.


To continue...
https://stackoverflow.com/questions/36870467/what-is-the-order-of-execution-in-javascript-promises

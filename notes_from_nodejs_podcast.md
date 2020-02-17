## Overview

Concepts of Nodejs' **Event Loop** aren't all that new and in the Posix world have existed for a long time. The idea is to act like a delegator for requests when you get them, so that request handling process can be unblocked. 

Nodejs callback based mechanism is handled at a low level by the libuv library which on a higher level use the **Select** and **Poll** system calls to listen to several File Descriptor changes and thereby react quickly to events in an Asychronous manner. This is nothing new though and some of the greatest wins come from **being able to use native JSON** at both Client and Server sides. From the APUE book, Sockets are also created like standard files and you get a File Descriptor. I think this ability allows Nodejs to handle multiple **Socket Connections** too which make it suitable for the Web RTC use cases.

Nodejs is therefore very good where you have a great deal of I/O going on. I don't really appreaciate the nitty gritty of this since I don't really understand the volume of I/O that a typical web request has to make. But I guess this consistutes disk reads, network I/O (REST API calls) or database calls etc.

Since I/O operations can be offloaded quickly with a Promise that this will be returned as soon as the result is available, the serving process is now free to listen to new requests.

**Important Note**

An important note here is that, while the I/O operations have been Async'd, the server still has to wait for the result of the I/O operation to serve it's response back. This makes async handling conceptually different from a **Work Queue** because even though tasks are being offloaded, in a **RabbitMQ** like model, the response is completed and the work is added to the background. 

So if you have credit card processing happening in the background, the response serving doesn't need to wait and you can still server the response with a reference back to the **background task**

Coming back to the main point, this still is a good win, since the request can continue doing what it can while the Async task has been offloaded to a queue. If your Async task requires a lot of Promise chaining then it may take a while to serve the result back. However, **the server process is still free to handle other requests**

## Comparissons to Thread Pool based model

In a traditional Java/C# land, to handle so many requests, you spawn say 1024 thread pool and each of these will handle the requests. This doesn't scale well if you have too many Requests Per Second and each request blocks the **handling thread** for a long time.

## Comparissons to Erlang/Elixir Process 

I think Erlang Processes can fundamentally beat what Nodejs really offers since we can spawn 100,000 of Elixir Processes so cheaply to be able to handle web requests. If I were to do a Benchmark, I think Elixir in theory could beat Nodejs. But I think practically Nodejs serves other use cases besides just building a **CRUD website**

## JSON handling

Typical handling of JSON that involves parsing and then treating that JSON data through layers of ORM introduces Latency to the application. This might be visible in say Mobile devices. 

if you imagine a stack where you have Nodejs and **MongoDB** as your data store, you have an end to end javascript based system. Fundamentally the **Data Model** on both the Client and Server side being the same, you can achieve some pretty big wins.


## Implications to Mobile and Other Resource Constrained Edges

The web world has changed in the presence of Mobile devices. What you have is apps running on the Client sending several events to the server or rather an API constantly. These could be scroll events etc. There is also the need to cache/offline data for the Client and sync it back when the Client is online. With an Isomorphic code base, the Client and Server's data models are identical and can therefore be exchanged. This is one of the use cases of Nodejs.

Also a typical SOAP request may take seconds to respond back which is too slow in the Mobile and Edge computing world.

There are tools like Browserify that deal with this Client/Server data model. It doesn't make the Client fat, but helps store the Server models at Client.

## Limitations

Immature transaction handling

## Summary 

With Nodejs based applications, one must think of modern evolutions, such as the Ubiquity of Mobile Devices and emergence of edge based IoT devices, which don't need traditional heavy Java and Relational database based systems. Concerns like **offline caching** and **memory consumption** are really important for these kind of use cases.

These systems are also **event based** and do a lot of **API** calls to get work done, for which Nodejs is a pretty good paradigm.

Nodejs also supports the **Isomorphic application** model where the data models on client and server side are same, such that they could be exchanged trivially. 

All in all Nodejs represents a need for modern applications and therefore many companies seem to be adopting it.

## References 
1. https://www.se-radio.net/2015/06/episode-230-shubhra-khar-on-nodejs/
2. https://nolanlawson.com/2017/05/22/a-brief-and-incomplete-history-of-javascript-bundlers/


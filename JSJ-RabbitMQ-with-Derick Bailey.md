What kind of things you want to have asynchronously with a web request ?
- sending an email 

Why do we care 
Performance, stability in your code, simplify the code because of decomposition 

unnecessary - database read requests
necessary - scheduling based things 

Redis gives you very simple pub-sub implementation, if you already have it already use it 
RabbitMQ works really well with pubsub advantages that you get additional messaging patterns and architectural patterns 

"That exchange looks at the metadata in all of its bindings and compares that metadata in the bindings with the metadata on the message that is being published. And it determines where that message should go. So, if you have for example an exchange called 'student' you might have a queue called students.enroll or something like that. And the names are arbitrary. You can call these things whatever you want. But you want to have a connection between that student exchange and the student enroll queue so that you can have code on the backend enroll students in whatever course they're supposed to be enrolling in. There's a relationship that you need in between those things. And you build that relationship with a binding"

Using for slack to compute the preview summary of the message after it has been sent (like URLs in messages)

Github.com example - creating a repo -- this doesn't happen in sync. Github uses redis to do all these sort of things.

Hard part is debugging 

Credit card is a classic example, where Stripe API has to do a lot of things in the background, the result of the operation being user getting an email. All this is intensive work which should never happen in a CRUD request.

RabbitMQ is not a cronjob, it is to distribute the work to other system. Your server is threaded to handle multiple requests but offload longer tasks to a work queue -- things that need to run async. Its like a distributed system where you call another process to do something for you and it is sometimes somewhat specialized.

You just let it fail, if you let it fail, it will just go back to the queue. This kind of reminds me of the erlang talk, conincidental that RabbitMQ is built of top of Erlang.

Pending
-----------------
RabbitMQ v/s websocket 

task queue vs message queue 


References
------------------
https://devchat.tv/js-jabber/170-jsj-rabbitmq-with-derick-bailey/

https://stackoverflow.com/questions/6636213/rabbitmq-vs-socket-io

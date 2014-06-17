LLC Javascript 2
===

Functions
$this
Closures & Callbacks
Events
How the event loop and callstack work together with all of this
jQuery and Frameworks: when and how to use

SystemXHR (closures, callbacks)
Parsing JSON

Review: 


There is another HTML file that you should have open in another tab called 'helpers.html' which contains some of the summary slides from Javascript I about variables, objects, and functions. A lot of the time when programmers are working they have open tabs in their browser that contain information about the language their working in. They don't have everything memorized, so don't think because you need to check the answer to something that you're not a 'real' programmer.

The first thing we're going to is review what we learned about functions last time, and then do a few exercises to warm up. Then, we're going to learn that there is a lot more to learn about functions.




Functions
===

- can be created via literals
- can be assigned to variables, array entries, and properties of other objects
- can be passed as arguments to functions
- can be returned as values from functions
- can possess properties that can be dynamically created and assigned
- functions are objects with a special property: they can be 'invoked' or 'executed'


Functions are the smallest, most modular unit of execution.

Most of the code we write will run as a result of functions. So, you can see they are very important if not the most important thing to master early in Javascript.

In Javascipt I we learned how to set up an event so that when we clicked on something, a function would be execute and it's code would be run. 

What happens if the browser has to deal with more than one event? How does it keep track of them? What if other code is running - other functions are running - and an event happens?

We're going to go through how your browser works with some diagrams so that you get an idea of what is happening. This way, when your code doesn't work, you have a high-level model for understanding what your browser is doing and where things went wrong.

Javascript is single-threaded: all this means is that when Javascript is working in the browser, only one thing can be done at a time. Only one function can be running at a time, even though we can write code to make it _seem_ like things are happening in parallel

Javascript is asynchronous: when we say this, we mean that Javascript can queue code up to be executed later. That means that is you do have many events that trigger, they will have to be run in the order the browser has the events triggered because as we just learned Javascript can only be running one thing at a time.

So: Javascript can only run one thing at a time, and when there is more than one function to run the browser has a way of figuring out what order things should happen in. As a result, functions can get queued up and this means that your code can execute later than you might expect. This has some side effects - both good and bad. 

Now, let's look at some examples and diagrams so that we can understand how this all works. 


The Browser Event Loop
===

Recall that the browser is a program too, written using code. We know that programs need to be told what to do. So what kind of program would we need to write in order to listen for user input? In order to be ready for user input, your browser is listening for input kind of like this:


Part of the programming inside your browser is a loop that continually listens for user input. User input triggers a piece of code to react. These are referred to as 'events'. 

Events are 



How Does Javascript _actually_ work?
===

"I understand the language, but how does it work? What's happening behind the scenes?"

A definition you might fund would read:

Javascript is a single-threaded non-blocking asynchronous concurrent runtime. <-- wat

Okay, that still doesn't really tell us what's happening.

JS Engine: Heap and Stack

Heap: Memory allocation
Stack: Execution contexts

The Callstack 

One thread == one callstack == one thing at a time

The callstack is basically how the JS runtime figures out what function is currently being executed and when finished that function, where does the value return to.

A stack is a data structure (just like arrays) with one interesting thing about it: you can only ever put things on top of it, or take things off the top of it. Unlike an array where you can insert a value at any index, you can only ever put things on the top of the stack, never in the middle or on the bottom.

File is kind of like main() context // go through example here of simple callstack
Go through call stack size exceeded

Blocking: What happens when things are slow?

Asynchronous Callbacks

Event Loop: If the stack is clear, and there is something in the callback queue, push the first thing in the queue onto the stack.

Think async: don't block the event loop

Scope
===

In the first Javascript I course, we learned about the 'global scope' and then 'function scope'.

Recall that 

closures = a room with one side transparent walls. You can see inside & outside but can't be seen from outside - @supersole


Closures and Callbacks
===


"Callbacks are just like children: they make you happiest when you give them names and plenty of room" - @maxogden, author of 'Javascript for Cats'


Hoisting
===

Let's take a look at these examples: [Angus' post examples are great](http://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/)

8, 3, 3 and [Type Error: bar is not a function]

Often around the internet, when looking at programming examples, you'll see the words 'foo', 'bar', and 'baz'.

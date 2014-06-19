LLC Javascript 2
===

Functions
Closures & Callbacks
Events
How the event loop and callstack work together with all of this
jQuery and Frameworks: when and how to use

SystemXHR (closures, callbacks)
Parsing JSON


Javascript is single-threaded: all this means is that when Javascript is working in the browser, only one thing can be done at a time. Only one function can be running at a time, even though we can write code to make it _seem_ like things are happening in parallel

Javascript is asynchronous: when we say this, we mean that Javascript can queue code up to be executed later. That means that is you do have many events that trigger, they will have to be run in the order the browser has the events triggered because as we just learned Javascript can only be running one thing at a time.

So: Javascript can only run one thing at a time, and when there is more than one function to run the browser has a way of figuring out what order things should happen in. As a result, functions can get queued up and this means that your code can execute later than you might expect. This has some side effects - both good and bad. 

Synchronous vs. Asynchronous
===

Use examples from [Raquel's post!](http://rckbt.me/2014/05/understanding-async/)


The Browser Event Loop
===

Recall that the browser is a program too, written using code. We know that programs need to be told what to do. So what kind of program would we need to write in order to listen for user input? In order to be ready for user input, your browser is listening for input kind of like this:


Part of the programming inside your browser is a loop that continually listens for user input. User input triggers a piece of code to react. These are referred to as 'events'. 


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

[Have a mini-quiz on how the browser works, multiple choice, here.]











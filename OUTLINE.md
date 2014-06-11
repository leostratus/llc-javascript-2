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


THe Browser Event Loop
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



Browser: 

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

[Have a mini-quiz on how the browser works, multiple choice, here.]







Function Declarations vs. Function Expressions
===

We're going to learn about a bit more nuance when it comes to how you write and use functions.

Recall that you can do this:


function doSomething(){
    // code to do something
};

doSomething();

or this

var doSomething = function() {
    // code to do something
};

doSomething();

Both of these will execute the code inside the curly braces. So how are they different?

The first example uses a function declaration. A function declaration defines a named function without requiring variable assignment.

Just like variable declarations start with 'var', function declarations must start with 'function'.

In this example, the function name is in available in the scope of it's function body, the stuff in the curly braces, and also in the parent scope of whatever contains it - whether that be a function you wrote, or the global scope. This is good, because how else would we call it?


The second example is called a 'function expression'. When a variable isn't declared on it's own using the function keyword, it is called a 'function expression'. This is a fancy way of saying that the function definiton, the stuff that says what the function will do, is a part of defining something else also. Sounds confusing? Let's think about this for a moment. In the first example, we're having the function defined all on it's own. In the second examplem we're seeing a function that is a store in a variable. Slightly different.

You can name the function expression or have it be anonymous. Anonymous functions are functions that do not have names. Javascript developers have different opinions on whether you should name your functions when you do this - I think you should because when you have a problem 

[put an example to show in the debugger here the difference between what debugging an anonymous vs named function expression is like]

var doSomething = function doingStuff(){
    // do some stuff!
};

In the case of a function assigned to a variable, the 'doingStuff' function name is not available in the parent scope of the variable it is assigned to.

Why not? It's inside the variable. The only way to call doStuff() is to call doSomething()!




Hoisting
===

Let's take a look at these examples: [Angus' post examples are great](http://javascriptweblog.wordpress.com/2010/07/06/function-declarations-vs-function-expressions/)

8, 3, 3 and [Type Error: bar is not a function]

Often around the internet, when looking at programming examples, you'll see the words 'foo', 'bar', and 'baz'. These words are just nonsense words designed to stand in for any identifier or name. 

function foo(){
    function bar() {
        return 3;
    }
    return bar();
    function bar() {
        return 8;
    }
}
alert(foo());

We've been talking about naming a bit, so let's look at this example here. There is a function foo, with two functions inside of it. They're both named bar. If we step line by line through this code, what number will be alerted?

If you said 3, well, your intuition was good. Except, it turns out that Javascript doesn't do that. Instead we have 8. Why did this happen?


Well, this works because the Javascript engine does operations to reorganize your Javascript when it encounters it.

It will take all of your function declarations and _move them to the top of the scope they are declared in_.

[I probably don't need to write our my internal monologue for all of this, I think I have this one down.]

//**Simulated processing sequence for Question 1**
function foo(){
    //define bar once
    function bar() {
        return 3;
    }
    //redefine it
    function bar() {
        return 8;
    }
    //return its invocation
    return bar(); //8
}
alert(foo());

What about function expressions, do they get hoisted too? How does this work if the function is inside a variable?

function foo(){
    var bar = function() {
        return 3;
    };
    return bar();
    var bar = function() {
        return 8;
    };
}
alert(foo());

Walkthrough:

//**Simulated processing sequence for Question 2**
function foo(){
    //a declaration for each function expression
    var bar = undefined;
    var bar = undefined;
    //first Function Expression is executed
    bar = function() {
        return 3;
    };
    // Function created by first Function Expression is invoked
    return bar();
    // second Function Expression unreachable
}
alert(foo()); //3








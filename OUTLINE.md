LLC Javascript 2
===

Functions
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


[Exercises Here]


Functions are the smallest, most modular unit of execution.

Most of the code we write will run as a result of functions. So, you can see they are very important if not the most important thing to master early in Javascript.

In Javascipt I we learned how to set up an event so that when we clicked on something, a function would be execute and it's code would be run. 

What happens if the browser has to deal with more than one event? How does it keep track of them? What if other code is running - other functions are running - and an event happens?

We're going to go through how your browser works with some diagrams so that you get an idea of what is happening. This way, when your code doesn't work, you have a high-level model for understanding what your browser is doing and where things went wrong.

Javascript is single-threaded: all this means is that when Javascript is working in the browser, only one thing can be done at a time. Only one function can be running at a time, even though we can write code to make it _seem_ like things are happening in parallel

Javascript is asynchronous: when we say this, we mean that Javascript can queue code up to be executed later. That means that is you do have many events that trigger, they will have to be run in the order the browser has the events triggered because as we just learned Javascript can only be running one thing at a time.

So: Javascript can only run one thing at a time, and when there is more than one function to run the browser has a way of figuring out what order things should happen in. As a result, functions can get queued up and this means that your code can execute later than you might expect. This has some side effects - both good and bad. 

Synchronous vs. Asynchronous
===

Use examples from [Raquel's post!](http://rckbt.me/2014/05/understanding-async/)

Synchronous Programming
===

You go to the shopping mall. Your first stop is to The Shirt Store. Having found the shirt you like, you go to the cashier, pay for your shirt, and walk out with your shirt. Next, you go to The Pants Store. Again, you pick out a pair of jeans, head to the cashier, pay, and walk out. Finally, you enter The Shoe Store. You grab your pair of shoes, pay for them at the cashier, and walk out. Now that you've got your shirt, pants, and shoes, you can go home and party on.

Asynchronous Programming
===

You are at home and are shopping online. You go to TheShirtStore.com, pick your shirt, and pay for it. Then you head to ThePantsStore.com, select your pants, and pay. Finally, you direct your browser to TheShoeStore.com and buy a pair of shoes. Over the course of the next week, your purchases show up via delivery. Your shoes come in first, then your shirt, and then your pants. Now that you've got your shirt, pants, and shoes, you can party on! (You don't need to go home, because you're probably home already.)


Now, let's look at some examples and diagrams so that we can understand how this all works. Then, we'll talk about how to manage functions when you're not sure when they'll execute.


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

Going Back to the Clothes Example
===

Let's go back to the clothes example where we had synchronous and asynchronous close purchases:

[examples]


Closures and Callbacks
===


"Callbacks are just like children: they make you happiest when you give them names and plenty of room" - @maxogden, author of 'Javascript for Cats'

Scope
===

In the first Javascript I course, we learned about the 'global scope' and then 'function scope'.


closures = a room with one side transparent walls. You can see inside & outside but can't be seen from outside - @supersole


[Exercises using callbacks with simple DOM APIs?]



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


Using variables to organize your code
===

As your Javascript programs get more complicated, this special way of defining functions inside of an object lets you organize your functions. 

Why is this important? Well, let's say you have some products and subscriptions on your website. Maybe you're running a web store and a blog for that store on the same website.

// Create an object to store our functions in, but we create named variables that represent categories of actions related to  

var products = {}; 
    
products.create = function(productName, price){
    // adds a new product to the website, let's pretend all products have unique names
};

products.destroy = function(productName){
    // removes a products from the website given the product name
};

var blog = {};

blog.create = function(blogText) {
    // adds a new blog post, gives it some kind of identifier like a unique ID/number or date
};

blog.destroy = function(blogID) {
    //destroys a blog post when given a valid ID for the blog post
};

We do this because we can't use the nice name of 'create' or 'destroy' more than once in a given scope. You could, in theory, do this:

function createProduct(productName, price)(){};
function destroyProduct(productName)(){};

function createBlogPost(blogText){};
function destroyBlogPost(blogID){};

I argue that putting your functions on objects and grouping them by what things they do and what they operate on is nicer and keeps them compartmentalized.



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

There is some Javascript magic here called 'hoisting'.

You'll notice in Javascript that you can do this:

baz();

function baz(){
    alert("Whoa, called the function before declaring it..? how does this magic work?");
}

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


Resources
===

Need to review the basics or know somebody who couldn't make it to Javascript I with you?

http://jsforcats.com/






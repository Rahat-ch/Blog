---
title: How JavaScript Works Part 1
date: '2019-04-24'
---

Welcome to Part 1 of my multi post series about “How JavaScript works”. This first post is going to focus primarily on two things: memory and the call stack. So we know that JavaScript is a program. There are two things a program needs to do: allocate memory then read and run commands. For JavaScript each browser has an engine (V8 in Chrome) that runs our JavaScript code. 

Let’s break this down a little further starting with memory. What is memory in JavaScript? In our case this is anytime you declare variables in your code. JavaScript remembers your declarations. Consider the code below:

```javascript

const coolDev = “Rahat”
const favoriteFood = “Steak”

```
After declaring these variables JavaScript now “remembers” (kind of like the North) that if it sees this variable coolDev then it’s set to this really cool dude named Rahat…or at least a string with his name in it. Same goes for favorite food it now knows that it’s Steak. Can you see a slight problem with this? The thing is declaring variables globally like this isn’t the best thing in the world. Memory is finite, and if you have a large application with a ton of global variables you might get what’s called a memory leak. You will eventually fill up the space allocated for memory and at that point you won’t be able to run your app in the browser. 

So we have a basic understanding of how memory works in JavaScript, let’s move on to part two of today’s post. The call stack! The call stack is very important to understand now as it directly affects parts of my future posts in this series. I highly recommend coming back to at least to this part of the post if you read any of my future posts in this series.

JavaScript is normally a single threaded language. This means it will run through the code and execute things line by line. Consider the code below.

```javascript

const coolDev = “Rahat”

console.log(`The coolest dev ever is ${coolDev}`)

```

If you aren’t familiar with template literals take a look at this page from <a href = https://developer.mozilla.org/en-US/docs/Web/JavaScript/Reference/Template_literals target="_blank">MDN</a>.

So what’s going on here? Well first my name is being stored in memory as a string for the variable coolDev. Then I execute a console.log. This fires up what’s called an execution context. JavaScript will create a list of things it needs to do, this is the call stack. In this code it’s just one simple thing we’re doing with console.log. Let’s add a couple more lines. 


```javascript

const coolDev = “Rahat”
const favoriteFood = “Steak”
const favoriteLanguage = “JavaScript”

console.log(`The coolest dev ever is ${coolDev}`)
console.log(`Rahat’s favorite food is ${favoriteFood}`)
console.log(`Rahat’s favorite language is ${favoriteLanguage}`)

```

So once again we’re allocating a bunch of variables to memory and now we have three console log statements. JavaScript will go through each line one by one and log each of these items, that’s our call stack. It does this really fast so it seems like its all being done instantly. Now remember that thing I mentioned called the execution context? Let’s take a deeper dive into that. 

```javascript

const whoIscool = () => {
console.log(“Rahat is cool”)
}

const favoriteFood = () => {
console.log(“Steak”)
}


const statement = () => {
whoIscool();
favoriteFood();
}

statement();

```
So again we’re allocating a few things to memory. In this case we have these three functions. Now how would JavaScript actually execute this code? You might say oh that’s simple it just goes line by line and executes things one by one! Well not quite...and I promise I didn’t lie to you in the last section. The thing is functions don’t actually get executed until we call them. We need to let JavaScript know “hey that function you have in your memory, yea go run that please!” So nothing actually starts executing until we hit the last line of code: statement();. 

When we call the statement function JavaScript remembers - “oh i have a function here named statement let’s see what’s inside.” We have now entered the execution context of the statement function! When it does get inside that function it sees that we call two additional functions and runs those one at a time. It starts with who is cool. But hey wait that is yet another function. We have now entered another execution context within the statement function! See the common thread here? We enter an execution context whenever a function is called. So in the who is cool function it runs a console log of “Rahat is cool”. 

The call stack in this execution context only had one thing so once it’s done we head out of the cool execution context back into the statement execution context. Now JavaScript will head to the next line and run the favorite food function. Guess what? We entered the execution context of the favorite food function! Now within this function we see once again we just have one thing in our call stack which is to log “Steak”. Once we finish here once again we’re back in the statement functions execution context and we see that there is nothing left in this call stack! Our code has completed its run. 

So there we have part one of “How JavaScript Works”. If you found this to be useful at all then I would love if you gave this post a share! I’m a firm believer in sharing knowledge and resources and would love to make a bigger impact on those starting off like I was several months ago. 

Keep an eye out for part two which will be put out some time next week after my blog post about this weekend's hackathon at Hack Fest NYC!
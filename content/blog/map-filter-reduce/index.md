---
title: Map, Filter, and Reduce
date: '2019-01-18'
---

Welcome to my first content filled post! Please note that I'm going to assume you have a basic understanding of ES6 for all of my blog posts. Free Code Camp has awesome stuff for learning ES6 if you need to brush up on it! I decided to start off with something that’s been giving me some trouble to master. JavaScript has a lot of cool features, one of those being Higher Order Functions. If you want the textbook definition, then this is a function that passes another function as an argument. Awesome now you fully understand what it means, right? Oh no, you don't? Yeah, I didn't really get it either at first. Let's take a look at three popular Higher Order functions: map, filter, and reduce.

Now all three of these are called array methods and are part of the array prototype. To understand prototype let’s dive into genetics for a second. I've been gifted with beautiful hazel-green eyes. It’s probably the only remotely attractive thing about me. Where did I get those from? My grandpa had those eyes and I inherited it through genetics passed down to me. JavaScript works the same way! An array has a prototype which all arrays inherit properties from!

Amazing, so now we know where map, filter, and reduce come from but why hell should we care? You're also wondering why I went into prototypes when this blog post is supposed to be about higher order functions. Well smart aleck, I think it’s important that you know that I'm not just grabbing these functions out of a hat. They come predefined in JavaScript and are waiting to help make your life easier.

Let's think about these functions by analyzing the day to day work of a car factory worker. These factories have what are called assembly lines. I am now going to give you a crude and likely very inaccurate description of how an assembly line works but bear with me, it should help!

## 1. Map

If you ever watched Dora the Explorer than you know that the map is a talking piece of paper that gives you instructions on where to go. Believe it or not, it works sort of the same way in JavaScript. You start with an array, Map will have some instructions in the form of a function and tell you to do something with the array and return a new one. Let's say we're on an assembly line and we need to create some cars, how would we do that? Well we start with a car shell and we have to insert an engine into it so it can run. (Yeah I know I'm highly knowledgeable about how cars are made).

So let's start with our Car shells:

```javascript
const carShells = ["Shell1", "Shell2", "Shell3"];
```

Amazing right? It's an Array of Car shells that we have to turn into real cars. We're given a map that tells us how to convert each of these into cars. They're all brought to us on conveyor belts:

```javascript
const cars = carShells.map(x => x + ' engine ')
```

Let's break down what this means:

Your car shells are coming down a conveyor belt (in this case the map function), and then you have a set of instructions that tell you to add an engine to your car shell. So we're adding the string ' engine' to each of the car shells. This is basically a for loop with added powers. If you were to log this to your console you should get the following result:

```javascript
Cars = ['Shell1 engine', 'Shell2 engine', 'Shell3 engine']
```

Great! So all of shells now have an engine. They are officially cars. You won't get the 'cars =' part, I just put that in there so it’s easier to visualize. If you work in the automobile industry, I apologize for any offense I may have caused you.

So a quick breakdown again of how that works:

- You start with an array
- Map will go through each item in the array
- If you pass in a function map will then follow the instructions of that function for each item of the array.
- A new array will be returned of the same length as the original.

For the next two examples please refer to the array of objects below:

```javascript
const inventory = [
  {
    car: 'civic1',
    color: 'blue',
    stock: 3,
  },
  {
    car: 'civic2',
    color: 'red',
    stock: 1,
  },
  {
    car: 'pilot1',
    color: 'purple',
    stock: 2,
  },
  {
    car: 'pilot2',
    color: 'red',
    stock: 1,
  },
]
```

## 2. Filter

Alright so now we know all about Dora's map...or well map in JavaScript I guess. Now filter is very similar. It works essentially the same way except instead of returning an array of the same size it does something to the array and spits back an array of equal or lesser length. What’s the thing it does you ask? Oh well it filters stuff. Perfect explanation right?

Anyway... we have our amazing inventory above, I am in no way associated to Honda, and we have a client who wants to buy all of our red cars. I don't ask questions as long as they pay top dollar. So you see each object in our array has three properties, a car, a color, and a stock quantity. Now at quick glance you might say "Rahat this is simple there are two red cars!". Well what if you had a legit inventory of hundreds or thousands of cars? How are you going to be able to eyeball that? You could but it'd be a waste of time when we have technology that can just do it for us.

Take a look at the function below:

```javascript
const redCars = inventory.filter(inventory => inventory.color === 'red')
```

So to find our red cars what we're going to do is send our inventory down a conveyer belt again, this time the conveyor belt is the filter function. Just like map it's going to do a magical loop through all of your inventory and check to see if any of the items matches up to the specs in the function you pass through it. In this case we have a function that tells us to check for any part of our inventory where the color is red.

If you log redCars now you should get this output:

```javascript
redcars = [{ car: 'civic2', color: 'red', stock: 1 }, { car: 'pilot2', color: 'red', stock: 1 }]
```

Amazing all of our red cars are all together and ready for our red car loving client!

So a quick recap again:

- You start with an array
- Filter will go through each item in the array
- If you pass in a function filter will then grab all the items that fulfill the requirements in that function.
- A new array will be returned of equal or lesser length than the original.

Pretty similar stuff to map, right?

## 3. Reduce

Feeling tired yet? I learned this and a whole bunch of other array methods in JS30 from Wes Bos. I highly recommend it if you really want to take your vanilla JavaScript skills to the next level. Without further ado here is the last array method of the day!

Now lets say there's an audit going on at your awesome car factory and you need to know how many cars you have total in your inventory. You can of course get all the values and put it all into a calculator and get that information. Or you can use reduce! What reduce does is takes an array and reduces that array down to just one value! Amazing how all these names can help us remember what the functions themselves do.

Let's consider the function below:

```javascript
const total = inventory.reduce(
  (stock, inventory) => (stock += inventory.stock),
  0
)
```

This one works slightly differently but is still just a magically powerful loop. This time we want to add up our total inventory so we use reduce and pass in the variables stock and inventory. You can use anything you like for the stock variable, you could name it banana for all I care but you should probably name it something that makes sense in this case like stock. Stock in this case is our accumulator, or the number at the end that our function will return for our total. The "+=" syntax you see here is just a quick and short way of saying "get the sum of all this stuff". The 0 at the end just specifies we're going to start from the beginning with 0 as our starting point.

You should get the lucky number 7 if you log this!

Another quick recap:

- You start with an array
- Reduce will go through each item in the array
- If you pass in a function reduce will know how to proceed in getting the array down to one value. In our case we let reduce know that it's going to have to add a few things for us.
- A single value will return based the function you specify.

There you have it, a quick and dirty explanation of Filter, Map, and Reduce. These are the most popular higher order functions and are the gateway drugs into functional programming. That’s a direct quote from Wes Bos. I’m sure you can tell by now that I’m a fan of his. Like I mentioned at the start, these higher order functions are all functions that pass in another function as an argument. For all of our methods we had a function that supplied us with the instructions for what each method actually needs to do. 

Here's a challenge for you guys:

Using the inventory array, return a new array of just the car names! If you figure it out send me a tweet @rahatcodes!
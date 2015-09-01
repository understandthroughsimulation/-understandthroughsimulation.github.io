The Monty Hall problem is a somewhat confusing one. From
[Wikipedia](https://en.wikipedia.org/wiki/Monty_Hall_problem), it can be
described as the following:

Suppose you're on a game show, and you're given the choice of three
doors: Behind one door is a car; behind the others, goats. You pick a
door, say No. 1, and the host, who knows what's behind the doors, opens
another door, say No. 3, which has a goat. He then says to you, "Do you
want to pick door No. 2?" Is it to your advantage to switch your choice?

It turns out that it is to your advantage to switch your choice. To
understand, let's begin simulating!

First, there's 3 doors:

    doors = c(1,2,3)

There's a door we pick, and a door with the car.

    # The sample(data,n) function will randomly select n items from data
    pick = sample(doors,1)
    car = sample(doors,1)

The goat door is one of the doors that isn't the one we picked and isn't
the one with the car.

    goat = sample(doors[! doors %in% c(pick,car)],1)

Now let's check if the door we picked is the one with the car

    pick == car

    ## [1] FALSE

Alright, well... if you actually picked the car or not it doesn't really
matter. It's not about doing this just once. We want to know which is
more likely. Lets try this again but lets run this problem 100 times.

    pickedCar = c()
    doors = c(1,2,3)
    for (i in 1:100) {
      pick = sample(doors,1)
      car = sample(doors,1)
      goat = sample(doors[! doors %in% c(pick,car)],1)
      pickedCar[i] = pick == car
    }

Ok, let's see it...How many times did I pick the right door?

    sum(pickedCar)/length(pickedCar)*100

    ## [1] 35

What?! That can't be true! Lets try 10,000 times.

    doors = c(1,2,3)
    for (i in 1:10000) {
      pick = sample(doors,1)
      car = sample(doors,1)
      goat = sample(doors[! doors %in% c(pick,car)],1)
      pickedCar[i] = pick == car
    }

And here we are...

    sum(pickedCar)/length(pickedCar)*100

    ## [1] 33.16

Okay. So what's going on here? The more times we run this, the closer we
get to 33.33..% but why's that? Well, it turns out that the chance of
car being in the other door is 2/3 and it being in the door you picked
is 1/3. Let's dive deeper.

When we first started, the odds of each door was 1/3 each. You knew if
you picked door number 1 you had a 1 in 3 chance of getting the car. You
also knew that there's a 2/3 chance that you don't get the car. What
that means is that there's a 2/3 chance of the car being behind door
number 2 or door number 3. Now when we prove that door number 3 has a
goat behind it, the chance of the car being behind door number 2 or 3
hasn't changed! Your knowledge has changed but the system hasn't.

It's still 1/3 chance the car is behind door number 1 and 2/3 chance
it's not which means that it's a 1/3 chance you picked correctly and a
2/3 chance you didn't. Switching to the other door means that your
chance of being correct is now 2/3 (just like the simulation shows).

Alright, that's it for this post on the Monty Hall problem. Let me know
if you have any questions in the comments section below. Also let me
know if there's other problems you would like to understand through
simulation!

Till next time.

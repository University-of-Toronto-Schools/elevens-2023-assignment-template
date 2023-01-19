# Elevens Card Game Assignment
## Introduction

The following activities are related to a simple solitaire game called Elevens. You will learn the rules of Elevens, and will be able to play it by using the supplied Graphical User Interface (GUI) shown below. You will learn about the design and the Object-Oriented Principles (OOP) that suggested that design. You will also implement much of the code.

 ![Elevens GUI](https://math.utschools.ca/wp-content/uploads/2023/01/01-gui.png)
 

## Activity 1: Design and Create a Card Class

### Introduction:
In this activity, you will complete a `Card` class that will be used to create card objects.

Think about card games you’ve played. What kinds of information do these games require a card object to “know”? 

What kinds of operations do these games require a card object to provide?

### Exploration:
Now think about implementing a class to represent a playing card. 

* What instance variables should it have?
* What data types are appropriate for the instance variables?
* What methods should be provided? 
* Should this class be mutable or immutable?

Discuss your ideas for this Card class someone in your class before implementing

### Implementation:
Complete the implementation of the provided `Card` class. You will be required to complete:
1)	Open BlueJ and start a new project called Elevens.
2)	Using the Edit menu, or the button on the left, make a new class called `Card`.
3)	Make sure your `Card` class has the following:
    * instance variables to represent the suit and rank of the card;
    * a constructor for the class;
    * getters for the instance variables (these should be called `getRank` and `getSuit`);
    * a method called `matches` that takes one parameter of type `Card` called `other` and returns `true` if `this` and `other` represent the same card.
4)	When you are done, check that it complies correctly and compare with someone else.  Note any differences and similarities between your solutions.
5)  <a name="test1" />Create several objects in your workspace:
    * create two objects that are identical (same rank and suit)
    * create another object that has the same rank, but different suit.
    * create another object that has the same suit as the two identical cards, but a different rank.
    * run the `matches` method and make sure that it gives the desired result
 

## Activity 2: Improving the Card class with `enum` 

### Introduction:
In the previous activity, we used `String`s to represent the rank and suit of a card.  This is bad design, since our intention is to have the rank be one of 13 values, and the suit one of 4 values.
Java provides a way to create new data types that can only have a predefined (finite) set of possible values called enumerated classes (or enums).
#### How enums work:
Below is the `.java` file for an enumeration that represents the months in a year.  A client class can then refer to these twelve constants as `Month.APRIL, Month.MAY`, etc.

```java
public enum Month
{
    JANUARY,
    FEBRUARY,
    MARCH,
    APRIL,
    MAY,
    JUNE,
    JULY,
    AUGUST,
    SEPTEMBER,
    OCTOBER,
    NOVEMBER,
    DECEMBER;
}
```

#### The `.values()` method
If you right-click on the Month enumerated class in BlueJ, you will see that it has three static methods, the first of which is `Month[] values()`.
This method returns an array of `Month`s **in the order they are declared in the `enum` definition**.	   

#### Other (non-`static`) methods
Each value of an enumerated class is itself an object, and Java provides several built-in methods. Two that will be useful for us are 
* `.name()` returns (as a `String`) the identifier of the constant, e.g. `Month.JULY.name()` returns `"JULY"`
*	`.ordinal()` returns (as an `int`) the number of the calling object, with respect to the order in which they were defined, e.g. `Month.JULY.ordinal()` returns 6 (not 7: in CS we start counting at zero).
 
### Instance Fields and the Constructor
Enumerated classes can also have instance fields, for example we can add a field for number of days in the month.  After adding your instance fields (declared `private final`), add a `private` constructor with a parameter for each instance field.  Then put the actual parameters in parentheses after each identifier (see example below).  You’ll probably want to access the data in the field, so add a “getter” as well.	  

```java
public enum Month
{
    JANUARY(31),
    FEBRUARY(28),
    MARCH(31),
    APRIL(30),
    MAY(31),
    JUNE(30),
    JULY(31),
    AUGUST(31),
    SEPTEMBER(30),
    OCTOBER(31),
    NOVEMBER(30),
    DECEMBER(31);
    
    private final int daysInMonth;
    
    private Month(int daysInMonth){
        this.daysInMonth = daysInMonth;
    }
    
    public int getDaysInMonth(){
        return daysInMonth;
    }
}
```

### Implementation:
1)	In the same project (folder) as your `Card` class, create two enumerated classes for `Suit` and `Rank`.
The Suit class should have four values: `CLUBS, DIAMONDS, HEARTS, SPADES`; the `Rank` class should have thirteen values: `ACE, TWO, THREE, FOUR, FIVE, SIX, SEVEN, EIGHT, NINE, TEN, JACK, QUEEN, KING`.
2)	Add a point value to the Rank class:
    * Add an integer (`int`) instance field to the `Rank` class called `pointValue`,
    * Assign the face value (1-10) for `ACE` through `TEN`, and zero for `JACK, QUEEN, KING`.
    * Write a (`private`) constructor to initialize the values.
    * Add a (`public`) "getter" method `getPointValue`.
3)	Update your `Card` class to use the `enum` types you have created.
4)	In the `Card` class, write a main method to re-implement the tests from Activity 1: Design and Create a Card Class.
5)	Add a method to the `Card` class called `print` that prints a `String` in the format `<*N*> of <*suit*>` if the rank of the card is TWO-TEN, and print “<rank> of <suit>” otherwise.  The string should be all lower case.
    **Notes**
    * enums can be used in switch statements.
    * use the name() method from enum
•	use the toLowerCase() method from String
6)	Add a call to print to your main method.
 
Activity 3: Initial Design of a Deck Class

Introduction:
A standard deck contains 52 cards, one of each rank/suit combination ( ).  In this Activity, you will write a Deck class that represents a collection of Cards 
Exploration:
What instance variables do you need to represent a deck of cards?



What methods should a deck object have?
Implementation:
1)	Create a new class Deck in the same folder as your Card class.
Your class should have two instance variables, An ArrayList of Cards called deck, and an integer called size.
•	The constructor should take two instance variables, an array of Rank and an array of Suit.
•	Use nested for loops to add one card of each rank/suit combination to your ArrayList. (You can use for-each loops here)
•	Initialize the size field to be the total number of cards in the deck.
•	Finally call the void method shuffle (to be implemented later).
2)	Add the following methods to your Deck class:
•	isEmpty: This method should return true when the size of the deck is 0; false otherwise.
•	size: This method returns the number of cards in the deck that are left to be dealt.
•	deal: This method “deals” a card by removing a card from the deck and returning it, if there are any cards in the deck left to be dealt. It returns null if the deck is empty. There are several ways of accomplishing this task. Here are two possible algorithms:
•	shuffle: just add a public void method with no contents for now.
Algorithm 1: Because the cards are being held in an ArrayList, it would be easy to simply call the method that removes an object at a specified index, and return that object. This algorithm also requires a separate “discard” list to keep track of the dealt cards. This is necessary so that the dealt cards can be reshuffled and dealt again.
Algorithm 2: Instead of removing the card, simply decrement the size instance variable and then return the card at size. In this algorithm, the size instance variable does double duty; it determines which card to “deal” and it also represents how many cards in the deck are left to be dealt. This is the algorithm that you should implement.
3)	Once you have completed the Deck class, add a main method to Deck and test the methods: 
•	create a deck, 
•	check the size, 
•	deal some cards, 
•	make sure the deck has the correct number of cards after dealing, 
•	deal the rest of the cards (while loop, using isEmpty),
•	 make sure deal returns null from an empty Deck.
4)	Explain in your own words the relationship between a Deck and a Card.
 

Activity 4: Shuffling the Cards in a Deck

Introduction:
Think about how you shuffle a deck of cards by hand. How well do you think it randomizes the cards in the deck?
Exploration:
We now consider the shuffling of a deck, that is, the permutation of its cards into a random-looking sequence. A requirement of the shuffling procedure is that any particular permutation has just as much chance of occurring as any other. We will be using the Math.random() method to generate random numbers to produce these permutations.
Several ideas for designing a shuffling method come to mind. We will consider two:
Perfect Shuffle
Card players often shuffle by splitting the deck in half and then interleaving the two half-decks, as shown below.


This procedure is called a perfect shuffle if the interleaving alternates between the two half-decks. Unfortunately, the perfect shuffle comes nowhere near generating all possible deck permutations. In fact, eight shuffles of a 52-card deck return the deck to its original state!
Consider the following “perfect shuffle” algorithm that starts with an array named cards that contains 52 cards and creates an array named shuffled.
•	Initialize shuffled to contain 52 “empty” elements. Set k to 0.
•	For j = 0 to 25,
o	Copy cards[j] to shuffled[k];
o	Set k to k+2. 
•	Set k to 1.
•	For j = 26 to 51,
o	Copy cards[j] to shuffled[k];
o	Set k to k+2.
This approach moves the first half of cards to the even index positions of shuffled, and it moves the second half of cards to the odd index positions of shuffled.
Selection Shuffle
The Knuth-Fisher-Yates Shuffle is a random shuffle, in that each card has an equally likely chance of ending up in a given position. For an array cards of length n:
•	for k = n-1 down to 1:
o	Generate a random integer r between 0 and k, inclusive;
o	Exchange cards[k] and cards[r]
This has the same structure as selection sort: For k = 51 down to 1,
•	Find r, the position of the largest value among cards[0] through cards[k];
•	Exchange cards[k] and cards[r].

The selection shuffle algorithm does not require to a loop to find the largest (or smallest) value to swap, so it works quickly.

Implementation:
1)	In the Deck class, add a public void method called perfectShuffle and implement the perfect shuffle algorithm from above.  This method should reset the size variable to the number of cards in the full deck.
2)	Implement the Selection shuffle in the body of the shuffle method you created earlier. (Don’t forget to reset the size variable.
3)	Test both methods, and in particular verify that eight perfect shuffles returns the deck to its original state.
4)	Modify your perfect shuffle algorithm so the original top card is now second from the top (make another method called inShuffle).  If implemented correctly, this should reverse the order of the deck after 26 shuffles!
 

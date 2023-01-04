# Rarity

## Overview

Since cards can be merged to create new ones, each card has a rarity. Creating rare cards require multiple merges. Even though the mechanics are simple, the math is thoughtful.

## Multiplication, Modulus and Prime Numbers

Alice has two cards #100 and #6.&#x20;

She can merge her cards to create Card ID #600

```
@dexoshi merge 100 6

will get card #600
```

Since there are 20,000 unique cards, what if Alice merges #11,000 and #2?

```
@deoshi merge 11000 3

will get card #13000
```

How? This is where modulus math (%) comes in

```
(cardA * cardB) % totalUniqueCards = mergedCard
```

or

```
(11000 * 3) % 20000 = 13000
```

## Card Rarity

Cards such as #100 are considered "common" because there are many ways players can merge to get #100:

```
1  * 100 = 100
2  * 50  = 100
4  * 25  = 100
5  * 20  = 20
10 * 10  = 100
```

ie [factorization](https://en.wikipedia.org/wiki/Factorization)

\#100 has more factors than #21

```
1 * 21 = 21
3 * 7  = 21
```

Since there are fewer options for #21 it will take significantly more work merging the correct card combinations to produce the desired #21.






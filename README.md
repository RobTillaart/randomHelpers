# randomHelpers

Arduino library for faster generation of random numbers.

## Description

This library contains functions that have the goal to deliver random bits faster
than the build in random function can, while still using it.

The idea is to have a buffer ( __randomBuffer) whcih can hold up to 32 bits.
When a number of random bits are needed, these are first fetched from the 
buffer and if the buffer gets empty, it if filled again with a call to random.

This strategy works well with a 32 bits buffer and requests for 1..16 random
bits. However above 16 bits the overhead is larger than the gain. So to improve
in that range too one could use a faster random function like the one from Marsaglia.

Note the gains differ per platform and are more explicit on the Arduino UNO platform
than on an ESP32. 

## Interface

functions implemented are

* **getRandom1()** returns 0 or 1, false or true. A wrapper exist called **flipCoin()**
* **getRandom6()** returns 0..31,
* **getRandom8()** returns 0..255 typically a byte
* **getRandom16()** returns 0..65535 (2 bytes)
* **getRandom24()** returns 0..16777215  (3 bytes)
* **getRandom32()** returns 0..2^32 - 1 (4 bytes) this is the core random generator
* **getRandomBits(n)** return 0.. 2^n - 1  This works well for 1..16 bits but above
it is slower than the standard way. 
* **throwDice()** returns 1..6, counts bits set in **getRandom6()** 

The examples show how to use these and how their performance gain relative to
calling **random()** for every random number.

## Future
* improve performance getRandomBits(n) for n = 17..31
* investigate new tricks :)
* wrap all up in a class.

## Operation

See examples

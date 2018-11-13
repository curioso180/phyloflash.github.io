---
layout: post
title: Structs in C
comments: true
---

Structs are widely used in C because it provides an "abstraction" type
for the programmer, trying to mimic what Object-Oriented-Programming
languages does.

Let's start with some struct definition.

```c

#include <stdint.h>

struct sensor_data {
    uint16_t temperature;
    uint16_t humidity;
    uint16_t brightness;
};
```
We could create this same data structure as a simple array, like this:

```c

#include <stdint.h>

#define TEMPERATURE (0)
#define HUMIDITY (1)
#define BRIGHTNESS (2)

#define SIZE (3)

uint16_t sensor_data[SIZE];

...

sensor_data[TEMPERATURE] = get_temperature();

```

This is much ugglier than using structures, beause we would need to know exactly each position what it means and etc... so, lets make it beautiful and simple.

To initialize strucutres, there are some nice ways to do that. We can initialize as if it is an arrray, or assigning by calling explicitly each one of the struct's field, like this:

```c

#include <stdint.h>

struct sensor_data data = {
    .temperature = 123;
    .humidity = 456;
    .brightness = 789;
};
```

## Unions in C

This is a pretty close friend of `struct`, but its behavior in memory is a bit different.
```c

#include <stdint.h>

union sensor_data data = {
    uint16_t temperature;
    uint16_t humidity;
    uint16_t brightness;
};
```

Unlike in `struct`, `union` does not arrange the data linearly in memory, but they are all located in the same address.

To give a better idea, if a `struct sensor_data` is initialized at `0x0100`, then the `temperature` is located at `0x0100`, humidity is located at `0x01010`, and brightness at `0x020`. However, `union` uses the same address region, so the members of a `union` acts just as aliases to the hsame address. So, temperature, humidity, and brightness will be all pointing to the same address, which is `0x0100`.

One interesting thing about `union` is that it does not need to have all data types the same size. Keep in mind that **the size of an `union` will be equal to the biggest field's size**. So, if the other data types are smaller, it will simply be truncated.

I will stop here. This may help someone out there.

### Disclaimer

I just downloaded the [Remarkable](https://remarkableapp.github.io/linux/download.html) **md** editor to see live modifications of the files, that is nice and I really recommend it.

## References

[1] [Unionize your variables: an introduction to advanced data types in c](https://hackaday.com/2018/03/02/unionize-your-variables-an-introduction-to-advanced-data-types-in-c/)

[2] [Remarkable](https://remarkableapp.github.io/linux/download.html)

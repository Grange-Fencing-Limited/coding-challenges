### Task 1

Create a function `maskify` to mask digits of a credit card number with `#`.

**Requirements:**

- Do not mask the first digit and the last four digits
- Do not mask non-digit chars
- Do not mask if the input is less than 6
- Return '' when input is empty

### Task 2

Create a function `number_to_ordinal` to create an ordinal number for a given input.
Ordinal numbers in English have something like `st`, `nd`, `rd`, etc.

**Requirements:**

- Apply for number 1 to 1001... if that works any given number will do ;-)

### Task 3

Create a calculator for [Reverse Polish Notation](https://en.wikipedia.org/wiki/Reverse_Polish_notation).
Write a `calculate` function that accepts an input and returns the result of the operation.

**Requirements:**

- Support the mathematical operations for `+`, `-`, `*` and `/`
- Check for invalid syntax, like `2 3+`. There is a space missing.
- Return 0 (integer) when nothing is entered
- Return the numeric value when no operand is given, like `1 2 3.5` return `3.5`

### Task 4

Given the following function you should suggest what could be improved. There are no other documents explaining why this function has been written or what the purpose is/should be.

**Example in python**

```python
def multiply(x, y):
    if y > 0:
        return (1 + multiply(x, y-1))
    else:
        return 0
```

**Possible considerations:**

- Does the function really _multiply_ two values?
    - Could the in-built multiply function be used?
    - Is a recursive function the way to go?
    - What can happen when using this with big numbers, f. ex. > 1.000.000?
    - Type hints

### Task 5

Do an in-place mirroring of a one dimensional array. In-place switching is key here as the input array can be very big
and no additional memory should be occupied - see [Space Complexity](https://www.geeksforgeeks.org/g-fact-86/).

**Requirements:**

- In-place mirroring
- Handle array with even and odd amount of items
- Do not use the [`array_reverse`](https://www.php.net/manual/de/function.array-reverse.php) function in PHP

**Example:**

- Even amount: `[8,5,1,4]` -> `[4,1,5,8]`
- Odd amount: `[6,2,7,9,3]` -> `[3,9,7,2,6]`
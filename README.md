# @steve02081504/bigfloat

A simple JavaScript library for arbitrary-precision arithmetic, also known as "bigfloat". This implementation is inspired by `elc`.

It allows you to work with very large numbers and high-precision decimals without floating-point inaccuracies. It represents numbers as fractions, enabling precise calculations.

## Features

-   **Infinite Precision:** Numbers are stored as fractions (numerator and denominator) for maximum precision.
-   **Basic Arithmetic:** Supports addition, subtraction, multiplication, division, modulus, and power operations.
-   **Comparisons:** Accurately compare numbers.
-   **String Conversion:** Handles conversion to and from strings, including support for repeating decimals (e.g., `0.3[3]`).
-   **Expression Evaluation:** Includes a built-in `eval` function to parse and compute mathematical expressions from a string.

## Installation

```bash
npm install @steve02081504/bigfloat
```

## Usage

### Basic Operations

```javascript
import { bigfloat } from '@steve02081504/bigfloat';

const a = bigfloat('10').div(bigfloat('3')); // 10/3
const b = new bigfloat('0.5'); // 1/2

console.log(a.toString()); // '3.[3]'
console.log(b.toString()); // '0.5'

// Addition
const sum = a.add(b);
console.log(sum.toString()); // '3.8[3]' (10/3 + 1/2 = 23/6)

// Multiplication
const product = a.mul(b);
console.log(product.toString()); // '1.[6]' (10/3 * 1/2 = 10/6)

// Negative numbers
const c = new bigfloat('-123.456');
console.log(c.neg().toString()); // '123.456'
```

### Repeating Decimals

The library can parse and represent repeating (recurring) decimals using bracket notation `[]`.

```javascript
import { bigfloat } from '@steve02081504/bigfloat';

// Parse a repeating decimal
const repeating = bigfloat('0.[1]'); // 1/9
console.log(repeating.toString()); // '0.[1]'

const result = repeating.mul(bigfloat('9'));
console.log(result.toString()); // '1'
```

### Expression Evaluation

Use the static `bigfloat.eval()` method to evaluate mathematical expressions from a string.

```javascript
import { bigfloat } from './main.mjs';

const result1 = bigfloat.eval('1.2 * (3.4 + 5.6)');
console.log(result1.toString()); // '10.8'

const result2 = bigfloat.eval('(1/3) + (2/7)');
console.log(result2.toString()); // '0.[428571]' (13/21)

const result3 = bigfloat.eval('2**100');
console.log(result3.toString()); // '1267650600228229401496703205376'
```

Supported operators in `eval`:
-   `+`, `-`, `*`, `/`, `%`, `**` (power)
-   `==`, `!=`, `<`, `>`, `<=`, `>=`
-   `&&`, `||`, `!` (logical)
-   Parentheses `()` for grouping.

## API

### `new bigfloat(value)`
Creates a new `bigfloat` instance. `value` can be a string, number, or another `bigfloat` instance.

### Arithmetic
-   `.add(other)`
-   `.sub(other)`
-   `.mul(other)`
-   `.div(other)`
-   `.mod(other)`
-   `.pow(other)`

### Comparison
-   `.equals(other)`
-   `.lessThan(other)`
-   `.greaterThan(other)`
-   `.compare(other)`: Returns `1` if greater, `-1` if less, `0` if equal.

### Other Methods
-   `.neg()`: Returns the negated value.
-   `.abs()`: Returns the absolute value.
-   `.floor()`: Returns the floor of the number.
-   `.toString()`: Converts the number to its string representation, using `[]` for repeating decimals.

### Static Methods
-   `bigfloat.eval(expression)`: Evaluates a mathematical expression string.
-   `bigfloat.fromString(string)`: Creates a `bigfloat` from a string.

# Java Loop Cheat Sheet

A compact reference covering classic `for`, enhanced `for-each`, `Iterable.forEach()`, iterators, `while`, `do-while`, increment operators, and streams.

## 1. Setup

```java
import java.util.Arrays;
import java.util.List;
import java.util.stream.IntStream;

List<Integer> numbers = Arrays.asList(10, 20, 30, 40, 50);
```

## 2. Classic `for` loop

Use this when you need the index, control over the increment, or to iterate backwards.

```java
// Iterate using an index
for (int i = 0; i < numbers.size(); i++) {
    System.out.println(numbers.get(i));
}

// Increment by 2
for (int i = 0; i < numbers.size(); i += 2) {
    System.out.println(numbers.get(i));
}

// Iterate backwards
for (int i = numbers.size() - 1; i >= 0; i--) {
    System.out.println(numbers.get(i));
}

// Count from 0 to 9
for (int i = 0; i < 10; i++) {
    System.out.println(i);
}
```

## 3. Enhanced `for` / for-each

The simplest option when you want to process every element.

```java
for (Integer number : numbers) {
    System.out.println(number);
}
```

Works with arrays, collections, and any object implementing `Iterable`.

```java
String[] names = {"Alice", "Bob", "Charlie"};

for (String name : names) {
    System.out.println(name);
}
```

## 4. Using `Iterable.forEach()` with a lambda

A concise alternative for collections.

```java
numbers.forEach(number -> System.out.println(number));

// Method reference: even shorter
numbers.forEach(System.out::println);
```

Note: `forEach()` is a method, not a `for` loop statement.

## 5. Using an `Iterator`

Useful when you need to traverse a collection explicitly or remove elements safely while iterating.

```java
var iterator = numbers.iterator();

while (iterator.hasNext()) {
    Integer number = iterator.next();
    System.out.println(number);
}
```

Removing elements safely:

```java
var iterator = numbers.iterator();

while (iterator.hasNext()) {
    if (iterator.next() < 30) {
        iterator.remove();
    }
}
```

After this example, `numbers` contains `30, 40, 50`.

## 6. `while` loop

Use this when the number of iterations isn't necessarily known in advance.

```java
int i = 0;

while (i < numbers.size()) {
    System.out.println(numbers.get(i));
    i++;
}
```

Infinite loop pattern (use with a termination condition or `break`):

```java
while (true) {
    // Do work

    if (someCondition()) {
        break;
    }
}
```

## 7. `do-while` loop

Executes the body **at least once**, even if the condition is initially false.

```java
int i = 0;

do {
    System.out.println(i);
    i++;
} while (i < 5);
```

## 8. Incrementing with `++`

The increment operator is often used inside a classic loop, but it can also be used independently.

```java
int i = 0;

i++;  // i is now 1
++i;  // i is now 2
i--;  // i is now 1
```

The difference matters when the expression's value is used:

```java
int a = 5;

System.out.println(a++); // Prints 5, then increments
System.out.println(++a); // Increments first, then prints 7
```

You can also use other increments:

```java
for (int i = 0; i <= 20; i += 5) {
    System.out.println(i); // 0, 5, 10, 15, 20
}
```

## 9. Java Streams

Streams are useful for transforming, filtering, and aggregating data. They are not simply a replacement for every loop.

### Basic stream iteration

```java
numbers.stream()
    .forEach(System.out::println);
```

### Filter elements

```java
numbers.stream()
    .filter(n -> n >= 30)
    .forEach(System.out::println);
```

### Transform elements with `map`

```java
numbers.stream()
    .map(n -> n * 2)
    .forEach(System.out::println);
```

### Calculate a sum

```java
int sum = numbers.stream()
    .mapToInt(Integer::intValue)
    .sum();
```

### Generate a numeric range without a collection

```java
IntStream.range(0, 5)
    .forEach(System.out::println); // 0 to 4

IntStream.rangeClosed(0, 5)
    .forEach(System.out::println); // 0 to 5
```

## 10. Quick comparison

| Approach | Best use case |
|---|---|
| Classic `for` | Index access, custom increments, reverse traversal |
| Enhanced `for` | Read every item in a collection or array |
| `Iterable.forEach()` | Concise lambda-based processing |
| `Iterator` | Explicit traversal and safe removal |
| `while` | Repeat while a condition holds |
| `do-while` | Execute at least once |
| `IntStream.range()` | Iterate over an integer range |
| `stream().filter().map()` | Transform and filter collections declaratively |

**Rule of thumb:** Use classic `for` when you need an index, enhanced `for` for straightforward iteration, and streams when expressing a data-processing pipeline. Avoid modifying a collection structurally inside a for-each loop; use an iterator or an appropriate collection method instead.

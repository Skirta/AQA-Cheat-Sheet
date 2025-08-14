# java_cheat_sheet

Core Java Concepts Cheat Sheet by :smile_cat:CattoDoesCode

### Table of Contents

* [Comments](#Comments)
* [Syntax](#Syntax)
* [Variables](#Variables)
* [String](#String)
* [If...Else](#Conditionals)
* [Switch](#Switch)
* [Loops](#Loops)
* [Array](#Array)
* [Method](#Method)
* [References](#References)

## Syntax

#### Main.java

```java
public class Main {

    public static void main(String[] args) {
	    // write your code here
    }
}
```

#### Printing a line to the console

```java
System.out.println("Hello World");
```

## Comments

#### Single-line Comment

```java
// This is a sample comment.
```

#### Multi-line Comment

```java
/* This is a sample
multi-line comment. */
```

## Variables

#### Primitive Data Types

| Data Type | Size   | Description                     | Range                                                                                                             |
|-----------|--------|---------------------------------|-------------------------------------------------------------------------------------------------------------------|
| `byte`    | 8-bit  | signed two's complement integer | `-128` to `127 `                                                                                                  |
| `short`   | 16-bit | signed two's complement integer | `-32,768` to `32,767`                                                                                             |
| `int`     | 32-bit | signed two's complement integer | -231 to  231-1 (i.e.,  `-2147483648` to `2147483647`)                                                             |
| `long `   | 64-bit | two's complement                | -263 to  263-1 (i.e.,  `-9223372036854775808` to `9223372036854775807                                             |
| `float`   | 32-bit | IEEE 754 floating point         | Negative range: `-3.4028235E+38` to `-1.4E-45` Positive range: `1.4E-45` to `3.4028235E+38`                       |
| `double`  | 64-bit | IEEE 754 floating point         | Negative range: `-1.7976931348623157E+308` to `-4.9E-324` Positive range: `4.9E-324` to `1.7976931348623157E+308` |
| `boolean` | 1-bit  | has only two possible values    | `true` or `false`                                                                                                 |
| `char`    | 16-bit | single 16-bit Unicode character | `'\u0000'` (or 0) to `'\uffff'` (or 65,535 inclusive)                                                             |

> `String` in Java is not a primitive data type but an object that are backed by char array. 

#### Declaring a Variable syntax:

```
<DataType> <variableName>;
```

_sample code:_

```java
int numVariable; // variable name is in camelCase
char my_variable; // variable name is in snake_case
```

#### Default Values

| Data Type               | Default Value |
|-------------------------|---------------|
| `byte`                  | 0             |
| `short `                | 0             |
| `int`                   | 0             | 
| `long`                  | 0L            | 
| `float`                 | 0.0f          |
| `double`                | 0.0d          |
| `char`                  | '\u0000'      |
| `boolean`               | false         |
| `String`(or any object) | null          |

#### Assigning a Variable a value:

```
<variableName> = <value or expression>;
```

_sample code:_

```java
numVariable = 100; 
my_variable = 'x'; // single quotation marks ('') for char and double quotation marks for string("")
```

## String

#### Creating a variable of type `String`

```java
String myString = "Java";
```

#### String Methods

| Method              | Description                                                                                                         |
|---------------------|---------------------------------------------------------------------------------------------------------------------|
| `lenth()`           | returns the length of characters inside the string                                                                  |
| `toUpperCase`       | converts a string into upper case                                                                                   |
| `toLowerCase`       | converts a string into lower case                                                                                   | 
| `indexOf("locate")` | returns the index (the position) of the first occurrence of a specified text in a string (including whitespace)     | 

> for more string methods: https://www.w3schools.com/java/java_ref_string.asp

_sample code:_

```java
public class Main {

    public static void main(String[] args) {
        String vowels = "AEIOU";
        System.out.println("length of vowels: " + vowels.length());
    }
}
```

_output:_
```
length of vowels: 5
```

## Conditionals

#### If, Else if, Else statement

_syntax:_

```java
if (condition1) {
    // block of code to be executed if condition1 is true
} 
else if (condition2) {
    // block of code to be executed if the condition1 is false and condition2 is true
} else {
    // block of code to be executed if the condition1 is false and condition2 is false
}
```

_sample code:_
```java
public class Main {
    public static void main(String[] args) {

        int x = 100;
        int y = 50;

        if (x < y) {
            System.out.println("x is less than y");
        }
        else if (x == y) {
            System.out.println("x is equal to y");
        }
        else {
            System.out.println("x is greater than y");
        }
    }
}
```

_output:_
```
x is greater than y
```

#### ternary operator

_syntax:_
```
variable = (condition) ? expressionTrue : expressionFalse  
```

_sample code:_
```java
public class Main {
    public static void main(String[] args) {

        int x = 100;
        int y = 50;

        String result = (x < y) ? "x is less than y" : "x is greater than y";
        System.out.println(result);

    }
}
```

_output:_
```
x is greater than y
```

## Switch

_syntax:_
```java
switch(expression) {
    case x:
        // code block
        break;
    case y:
        // code block
        break;
    default:
        // code block
}
```

> The `break` keyword terminates a switch statement or a loop statement.

_sample code:_

```java
public class Main {
    public static void main(String[] args) {

        int choice = 3;
        switch(choice) {
            case 1:
                System.out.println("one");
                break;
            case 2:
                System.out.println("two");
                break;
            case 3:
                System.out.println("three");
                break;
        }

    }
}
```

#### enhanced switch statement

```java
public class Main {
    public static void main(String[] args) {

        int choice = 3;
        switch (choice) {
            case 1 -> System.out.println("one");
            case 2 -> System.out.println("two");
            case 3 -> System.out.println("three");
        }

    }
}
```

_output:_

```
three
```



## Loops

#### for loop

_syntax:_
```java
for ((initialization); (condition); (increment)) {
    // code block to be executed
}
```

_sample code:_

```java
public class Main {
    public static void main(String[] args) {

        for (int i = 0; i <= 10; i+=1) {
            System.out.println(i);
        }

    }
}
```

_output:_

```
0
1
2
3
4
5
6
7
8
9
10
```

#### while loop

_syntax:_
```java
while(condition) {
    // code block to be executed    
}
```

_sample code:_

```java
public class Main {
    public static void main(String[] args) {

        int i = 0;
        while(i <= 10) {
            System.out.println(i);
            i++;
        }

    }
}
```

_output:_

```
0
1
2
3
4
5
6
7
8
9
10
```

#### do while loop

_syntax:_
```java
do {
        // code block to be executed
}
while (condition);
```

_sample code:_

```java
public class Main {
    public static void main(String[] args) {

        int i = 0;
        do {
            System.out.println(i);
            i++;
        }
        while(i <= 10);

    }
}
```

_output:_

```
0
1
2
3
4
5
6
7
8
9
10
```

## Array

#### Creating an Array 

_syntax:_
```
<dataType>[] <variable> = <value>;
```

_sample code:_

```java
String[] ones = ["one", "two", "three", "four", "five", "six", "seven", "eight", "nine", "ten"]
```

#### Access Array elements

```java
public class Main {
    public static void main(String[] args) {

        int[] tens = {10, 20, 30, 40, 50, 60, 70, 80, 100};
        System.out.println(tens[2]);

    }
}
```

_output:_
```
30
```

#### Change Array elements

```java
public class Main {
    public static void main(String[] args) {

        int[] tens = {10, 20, 30, 40, 50, 60, 70, 80, 100};
        tens[8] = 90;
        System.out.println(tens[8]);

    }
}
```

_output:_
```
90
```

#### Loop through an Array

```java
public class Main {
    public static void main(String[] args) {

        String[] days = {"Monday", "Tuesday", "Wednesday", "Thursday", "Friday", "Saturday", "Sunday"};

        for (String d : days) {
            System.out.println(d);
        }
        
    }
}
```

_output:_
```
Monday
Tuesday
Wednesday
Thursday
Friday
Saturday
Sunday
```

## Method

#### Creating a Method syntax

```
static <void> <methodName>() {
    // code to be executed    
}
```

_keywords:_
> `static` means that the method belongs to the Main class and not an object of the Main class.
> `void` means that this method does not have a return value.

or

```
static <dataType> <methodName>() {
    // code to be executed  
    return <value or expression>  
}
```

> If you want the method to return a value, you can use a primitive data type (such as `int`, `char`, etc.) instead of `void`, and use the `return` keyword inside the method:

#### void method
_sample code:_
```java
public class Main {
    static void hello_world(){
        System.out.println("Hello, world!");
    }

    public static void main(String[] args) {
        hello_world();
    }
}
```

_output:_
```
Hello, world!
```

#### value-returning method
_sample code:_
```java
public class Main {
    static String greet_user(String user){
        return "Hello, " + user;
    }

    public static void main(String[] args) {
        System.out.println(greet_user("Bob"));
    }
}
```

_output:_
```
Hello, Bob
```

<br/><br/>

### References

* Java Documentation | [docs.oracle.com](https://docs.oracle.com/javase/tutorial/java/nutsandbolts/datatypes.html "Java Documentation")
* [mathcenter.oxford.emory.edu](http://mathcenter.oxford.emory.edu/site/cs170/variables/#:~:text=There%20are%208%20primitive%20types,double%2C%20boolean%2C%20and%20char. "Variables and the 8 Primitive Data Types")
* [w3schools.com](https://www.w3schools.com/java/default.asp "Java Tutorial")
* [javatpoint.com](https://www.javatpoint.com/java-tutorial "Java Tutorial")
* [geeksforgeeks.org](https://www.geeksforgeeks.org/strings-in-java/#:~:text=Strings%20in%20Java%20are%20Objects,entirely%20new%20String%20is%20created.)


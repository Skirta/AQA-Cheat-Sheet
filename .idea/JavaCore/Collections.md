#### Колекції
_Колекції_ — це набір класів та інтерфейсів у Java, які дозволяють зберігати та маніпулювати групами об'єктів.  
Колекції є більш гнучкими та потужними, ніж звичайні масиви.

Існує три основні інтерфейси колекцій: `List`, `Set` та `Map`.

| Інтерфейс | Особливості | Приклади реалізації |
|:----------| :--- | :--- |
| List      | _Упорядкований список, що дозволяє зберігати дублікати. Елементи мають індекс, як у масиві_. | `ArrayList`, `LinkedList` |
| Set       | _Невпорядкована колекція, що зберігає лише унікальні елементи._ | `HashSet`, `TreeSet` |
| Map       | _Зберігає дані у форматі "ключ-значення". Кожен ключ є унікальним, а значення можуть повторюватися._ | `HashMap`, `TreeMap` |

#### List (на прикладі `ArrayList`)
`List` — це впорядкована колекція, яка може містити дублікати. Елементи доступні за індексом.
```java
import java.util.ArrayList;
import java.util.List;

// Створення ArrayList
List<String> cities = new ArrayList<>();

// Додавання елементів
cities.add("Київ");
cities.add("Львів");
cities.add("Київ"); // Дублікати дозволені

// Доступ до елементів за індексом
String firstCity = cities.get(0); // "Київ"
String thirdCity = cities.get(2); // "Київ"

// Видалення елемента за значенням
cities.remove("Львів");

// Видалення елемента за індексом
cities.remove(0); // Видаляє "Київ"

// Перевірка наявності елемента
boolean containsCity = cities.contains("Київ"); // true

// Отримання розміру
int size = cities.size(); // size = 1
```
#### Set (на прикладі `HashSet`)
`Set` — це невпорядкована колекція, яка зберігає лише унікальні елементи. Дублікати ігноруються.
```java
import java.util.HashSet;
import java.util.Set;

// Створення HashSet
Set<String> uniqueColors = new HashSet<>();

// Додавання елементів
uniqueColors.add("Red");
uniqueColors.add("Green");
uniqueColors.add("Red"); // Дублікат ігнорується

// Перевірка наявності елемента
boolean hasGreen = uniqueColors.contains("Green"); // true

// Видалення елемента
uniqueColors.remove("Green");

// Розмір колекції
int size = uniqueColors.size(); // size = 1

// Ітерація по елементах
for (String color : uniqueColors) {
System.out.println(color);
}
```
#### Map (на прикладі `HashMap`)
`Map` — це колекція, яка зберігає дані у форматі "ключ-значення". Кожен ключ є унікальним, а значення можуть повторюватися.

```java
import java.util.HashMap;
import java.util.Map;

// Створення HashMap
Map<Integer, String> students = new HashMap<>();

// Додавання пар "ключ-значення"
students.put(1, "Олег");
students.put(2, "Марія");
students.put(1, "Андрій"); // Значення для ключа 1 буде перезаписано

// Отримання значення за ключем
String studentName = students.get(1); // "Андрій"

// Перевірка наявності ключа
boolean hasKey = students.containsKey(2); // true

// Видалення пари за ключем
students.remove(1);

// Отримання розміру
int size = students.size(); // size = 1
```
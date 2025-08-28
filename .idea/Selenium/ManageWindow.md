# 🖥️ Керування вікнами (Manage Window)
Selenium WebDriver надає методи для керування розміром, позицією та станом вікна браузера.  
Це особливо корисно при тестуванні адаптивного дизайну або коли потрібно працювати з кількома вікнами.
---
#### 📌 Основні методи керування вікнами

| Метод                                                      | Опис                                                    |
|-------------------------------------------------------------|---------------------------------------------------------|
| `driver.manage().window().maximize()`                       | Розгортає вікно браузера на весь екран.                 |
| `driver.manage().window().fullscreen()`                     | Переводить вікно браузера в повноекранний режим (F-11). |
| `driver.manage().window().minimize()`                       | Згортає вікно браузера.                                 |
| `driver.manage().window().setSize(new Dimension(width, height))` | Встановлює розмір вікна браузера в пікселях.            |
| `driver.manage().window().setPosition(new Point(x, y))`     | Встановлює позицію вікна браузера на екрані.            |
| `driver.manage().window().getSize()`                        | Отримує поточний розмір вікна браузера.                 |
| `driver.manage().window().getPosition()`                    | Отримує поточну позицію вікна браузера.                 |

---
#### 🧠 Порада
Методи maximize(), minimize() і fullscreen() змінюють стан вікна, що може вплинути на розташування елементів.  
Завжди перевіряйте, чи всі елементи залишаються видимими після зміни розміру.

---
#### 📘 Приклад використання
```java
import org.openqa.selenium.Dimension;
import org.openqa.selenium.Point;

// Розгортання вікна на весь екран
driver.manage().window().maximize();

// Встановлення конкретного розміру вікна (наприклад, для тестування адаптиву)
driver.manage().window().setSize(new Dimension(800, 600));

// Отримання поточного розміру
Dimension size = driver.manage().window().getSize();
System.out.println("Ширина: " + size.getWidth() + ", Висота: " + size.getHeight());

// Встановлення позиції вікна
driver.manage().window().setPosition(new Point(10, 50));

// Отримання поточної позиції
Point position = driver.manage().window().getPosition();
System.out.println("X: " + position.getX() + ", Y: " + position.getY());

// Перехід у повноекранний режим
driver.manage().window().fullscreen();
```

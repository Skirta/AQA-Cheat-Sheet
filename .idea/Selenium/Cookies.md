# 🍪 Робота з Cookies
Цей розділ пояснює, як взаємодіяти з файлами cookie за допомогою Selenium.  
Це корисно для тестування авторизації, персоналізації та збереження сесії.
---
#### 📌 Основні методи для роботи з Cookies

| Метод                                      | Опис                                                        |
|--------------------------------------------|-------------------------------------------------------------|
| `driver.manage().addCookie(cookie)`        | Додає файл cookie до поточного домену.                      |
| `driver.manage().getCookieNamed("name")`   | Отримує файл cookie за його іменем.                         |
| `driver.manage().getCookies()`             | Отримує всі файли cookie для поточного домену як `Set<Cookie>`. |
| `driver.manage().deleteCookie(cookie)`     | Видаляє вказаний файл cookie.                               |
| `driver.manage().deleteCookieNamed("name")`| Видаляє файл cookie за його іменем.                         |
| `driver.manage().deleteAllCookies()`       | Видаляє всі файли cookie для поточного домену.              |

---
#### 🧠 Порада
Перед тим, як додавати, отримувати або видаляти файли cookie, переконайся, що ти перебуваєш на тому самому домені, для якого призначений cookie.  
В іншому випадку, методи можуть не спрацювати.

---
#### 📘 Приклад використання
```java
import org.openqa.selenium.Cookie;
import java.util.Set;

// Створення об'єкта Cookie
Cookie cookie = new Cookie("mycookie", "somevalue");

// Додавання cookie до поточної сторінки
driver.manage().addCookie(cookie);

// Отримання всіх cookie та друк їх імен та значень
Set<Cookie> allCookies = driver.manage().getCookies();
for (Cookie c : allCookies) {
System.out.println(c.getName() + " : " + c.getValue());
}

// Отримання cookie за іменем
Cookie myCookie = driver.manage().getCookieNamed("mycookie");
System.out.println("Значення 'mycookie': " + myCookie.getValue());

// Видалення cookie за іменем
driver.manage().deleteCookieNamed("mycookie");

// Видалення всіх cookie
driver.manage().deleteAllCookies();
```
# 📄 Document Object Model (DOM)  
Цей розділ пояснює, як Selenium взаємодіє з елементами на веб-сторінці за допомогою DOM.

---
#### 📌 Ключові концепції DOM  
| Термін       | Опис                                                                                           |
|--------------|------------------------------------------------------------------------------------------------|
| `Document`   | Веб-сторінка, яку WebDriver завантажив у вікно. Кожен document має ієрархію елементів.         |
| `Element`    | Кожен HTML-тег (наприклад, `<div>`, `<p>`, `<a>`) на веб-сторінці є елементом DOM.             |
| `Node`       | Усі об'єкти в DOM-ієрархії: елементи, атрибути, текстові вузли.                                |
| `By Class`   | Клас в Selenium, що використовується для пошуку елементів. Забезпечує статичні методи, такі як `By.id()`, `By.name()`, `By.className()`, тощо. |
| `WebElement` | Об'єкт, що представляє елемент HTML. Після знаходження елемента, ви можете взаємодіяти з ним, викликаючи методи `click()`, `sendKeys()`, `getText()`, тощо. |

---
#### 🧠 Порада  
DOM може динамічно змінюватися за допомогою JavaScript.  
Використовуйте явні очікування (`Explicit Waits`), щоб переконатися, що елемент став доступним або видимим, перш ніж намагатися з ним взаємодіяти.  
Це допоможе уникнути помилок типу `NoSuchElementException`.

---
#### 📘 Приклад використання
```java
// Знаходження елемента за ID та натискання на нього
WebElement loginButton = driver.findElement(By.id("login-button"));
loginButton.click();

// Знаходження текстового поля за іменем та введення тексту
WebElement usernameField = driver.findElement(By.name("username"));
usernameField.sendKeys("testuser");

// Отримання тексту з елемента
WebElement welcomeMessage = driver.findElement(By.tagName("h1"));
String messageText = welcomeMessage.getText();
System.out.println(messageText);

// Знаходження елементів за CSS-селектором
WebElement link = driver.findElement(By.cssSelector("a.nav-link"));
link.click();
```
# 🖼️ Робота з `iframe` у Selenium

---

#### ❓ Що таке `iframe`
`iframe` (**inline frame**) – це HTML-елемент, який вбудовує **іншу вебсторінку всередину поточної**.  
Він створює **окремий DOM** (документ усередині документа).  
👉 Щоб взаємодіяти з елементами всередині `iframe`, **потрібно спочатку переключитися у цей фрейм**, інакше Selenium не зможе знайти елементи.

---

#### 📌 Основні методи роботи з фреймами

| Метод | Опис |
|------|------|
| `driver.switchTo().frame(int index)` | Перемикає драйвер у `iframe` за індексом (0 – перший фрейм на сторінці). |
| `driver.switchTo().frame(String nameOrId)` | Перемикає за атрибутом `name` або `id` у тегу `<iframe>`. |
| `driver.switchTo().frame(WebElement frameElement)` | Перемикає через об’єкт `WebElement`, що представляє сам `<iframe>`. |
| `driver.switchTo().parentFrame()` | Повертає управління на **батьківський** фрейм (на один рівень вище). |
| `driver.switchTo().defaultContent()` | Повертає управління на **основний документ** (повністю вихід з усіх фреймів). |

---

#### 📘 Приклади використання

##### 🔹Перемикання за індексом
```java
// Перемикаємось на перший iframe на сторінці
driver.switchTo().frame(0);

// Пошук елемента всередині iframe
driver.findElement(By.id("button")).click();

// Повернення до головного документа
driver.switchTo().defaultContent();
```
---
##### 🔹Перемикання за ім’ям або ID
```java
// Якщо iframe має атрибут name="myFrame"
driver.switchTo().frame("myFrame");
driver.findElement(By.name("search")).sendKeys("Selenium");
driver.switchTo().defaultContent();
```
---
##### 🔹 Перемикання за WebElement
```java
WebElement iframe = driver.findElement(By.cssSelector("iframe[src*='login']"));
driver.switchTo().frame(iframe);
driver.findElement(By.id("username")).sendKeys("testuser");
driver.switchTo().defaultContent();
```
---
##### 🔹 Вкладені (nested) фрейми
```java
// Перемикаємось на батьківський iframe
driver.switchTo().frame("parentFrame");
// Потім у внутрішній iframe
driver.switchTo().frame("childFrame");
// Дії з елементами
driver.findElement(By.id("innerBtn")).click();
// Повертаємось до основного документа
driver.switchTo().defaultContent();
```
---
#### 🧠 Поради та нюанси
- Якщо елемент не знаходиться – перевір, чи він не всередині iframe.  
- Використовуй defaultContent(), якщо потрібно повністю повернутися до початкової сторінки, а не лише на один рівень вище.  
- Переконайся, що фрейм вже завантажений. Можна використати Explicit Wait для очікування:
```java
new WebDriverWait(driver, Duration.ofSeconds(10))
    .until(ExpectedConditions.frameToBeAvailableAndSwitchToIt("myFrame"));
```
Цей метод одночасно очікує появу фрейму та перемикає у нього.

---
#### 💡 Перевірка через DOM  
У DevTools шукай теги:
```java
<iframe src="..." id="frame1" name="frameName"></iframe>
```
Все, що знаходиться всередині цього тега, потребує `switchTo().frame(...)` для доступу.

---
#### 🔑 Основне правило
Щоб працювати з елементом усередині iframe:
- Перемкнись у фрейм (frame(...)).  
- Виконай дію (клік, введення тексту тощо).  
- Повернись назад у основний документ (defaultContent() або parentFrame()).  
Без цього Selenium видасть NoSuchElementException.
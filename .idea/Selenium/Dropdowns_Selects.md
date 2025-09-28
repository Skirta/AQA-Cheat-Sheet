# ⬇️ Робота з випадаючими списками у Selenium

#### ❓ Що таке Dropdown / Select
- **Стандартний `<select>`** – HTML-елемент із тегом `<select>` і `<option>`.  
  ✅ Selenium має вбудований клас `Select` для зручної роботи.
- **Кастомний dropdown** – HTML-список, стилізований під випадаючий (наприклад, `<div>`, `<ul>`).  
  ❌ Клас `Select` тут **не працює**, взаємодія виконується як зі звичайними елементами (кліки, Actions).

---

#### 📌 Основні методи класу `Select`

| Метод | Опис |
|------|------|
| `new Select(WebElement element)` | Створює об’єкт `Select` для роботи зі стандартним `<select>`. |
| `selectByVisibleText(String text)` | Вибір опції за **видимим текстом** (наприклад `"Option 1"`). |
| `selectByValue(String value)` | Вибір опції за атрибутом `value` у `<option>`. |
| `selectByIndex(int index)` | Вибір опції за порядковим номером (починаючи з 0). |
| `deselectByVisibleText(String text)` | Зняття вибору за видимим текстом (для **multi-select**). |
| `deselectByValue(String value)` | Зняття вибору за `value`. |
| `deselectByIndex(int index)` | Зняття вибору за індексом. |
| `deselectAll()` | Знімає вибір з усіх опцій (для **multi-select**). |
| `getOptions()` | Повертає `List<WebElement>` зі всіма `<option>`. |
| `getAllSelectedOptions()` | Повертає `List<WebElement>` з усіма вибраними опціями. |
| `getFirstSelectedOption()` | Повертає перший вибраний елемент (корисно для single-select). |
| `isMultiple()` | Перевіряє, чи підтримується вибір кількох опцій (**multi-select**). |

---

#### 📘 Приклади використання

##### 🔹 Базова робота зі стандартним `<select>`
```java
WebElement selectElement = driver.findElement(By.id("country"));
Select country = new Select(selectElement);

// Вибір за видимим текстом
country.selectByVisibleText("Poland");

// Вибір за value
country.selectByValue("PL");

// Вибір за індексом
country.selectByIndex(2);
```
---
##### 🔹 Отримання всіх опцій
```java
List<WebElement> allOptions = country.getOptions();
for (WebElement option : allOptions) {
    System.out.println(option.getText());
}
```
---
##### 🔹 Перевірка та вибір кількох значень (multi-select)
```java
WebElement skillsElement = driver.findElement(By.id("skills"));
Select skills = new Select(skillsElement);

if (skills.isMultiple()) {
    skills.selectByVisibleText("Java");
    skills.selectByVisibleText("Python");

    // Отримати всі вибрані опції
    List<WebElement> selected = skills.getAllSelectedOptions();
    for (WebElement s : selected) {
        System.out.println("Selected: " + s.getText());
    }

    // Зняти вибір
    skills.deselectAll();
}
```
---
#### 🎯 Робота з кастомними dropdown'ами
```java
// Відкрити меню
driver.findElement(By.cssSelector(".dropdown-toggle")).click();

// Натиснути на потрібну опцію
driver.findElement(By.xpath("//li[text()='Option 2']")).click();
```
Для складних кастомних меню іноді корисні:
- Actions.moveToElement(...) для hover.  
- WebDriverWait для очікування появи списку.  
---
#### ⏳ Очікування опцій  
Щоб дочекатися завантаження опцій перед вибором:
```java
new WebDriverWait(driver, Duration.ofSeconds(10))
    .until(ExpectedConditions.presenceOfElementLocated(By.id("country")));
```
---
#### 🧠 Поради  
1. Використовуй isMultiple() перед спробою вибору кількох значень, інакше отримаєш UnsupportedOperationException.
2. selectByIndex() може бути крихким, якщо порядок опцій змінюється – краще використовувати selectByValue() або selectByVisibleText().
3. Для динамічних списків (наприклад, завантаження через AJAX) комбінуй WebDriverWait із ExpectedConditions.
# 🎮 1. Клас Actions  

`Actions` використовується для симуляції складних дій користувача: робота з мишею, клавіатурою, drag & drop.   
Він дозволяє будувати ланцюжки дій і виконувати їх.  
---
🔎 Виконання дій: `.perform()` vs `.build()`

`.perform()` – одразу виконує зібраний ланцюжок дій.  
У Selenium (3.0+ або 4.0+) цього методу достатньо – він автоматично викликає `.build()` під капотом.

```java
actions.moveToElement(menu).click().perform(); // ✅ найпоширеніший варіант
```

`.build()` – явно створює об’єкт Action із зібраних дій.  
Використовуй, коли потрібно:
- зберегти набір дій і виконати його пізніше;
- повторити одні й ті самі дії кілька разів.
```java
Action hoverAndClick = actions.moveToElement(menu).click().build();
hoverAndClick.perform(); // виконання збереженого Action
```
📝 У більшості випадків використовуй просто .perform(), а .build() застосовуй лише тоді, коли треба мати контроль над створеним Action-ланцюжком.  

---
#### 📌 Основні методи `Actions`

| Метод | Опис |
|-------|------|
| `click()` | Виконує клік лівою кнопкою миші у поточній позиції курсора. Може викликатися без параметрів або з `WebElement` (`click(element)`) для кліку по елементу. |
| `doubleClick()` | Подвійний клік у поточній позиції курсора. Може приймати `WebElement` (`doubleClick(element)`). |
| `contextClick()` | Виконує правий клік (відкриває контекстне меню). Може викликатися без параметрів або з `WebElement` (`contextClick(element)`). |
| `moveToElement(element)` | Наводить курсор на вказаний `WebElement`. Використовується для hover-ефектів або меню. |
| `moveByOffset(x, y)` | Переміщує курсор на вказані координати (відносно поточного положення). |
| `dragAndDrop(source, target)` | Перетягує елемент `source` і відпускає його над `target`. |
| `dragAndDropBy(source, xOffset, yOffset)` | Перетягує елемент `source` на вказане зміщення. |
| `clickAndHold(element)` | Затискає ліву кнопку миші на елементі (але не відпускає). Використовується для складних drag & drop. |
| `release()` | Відпускає затиснуту кнопку миші (завершує `clickAndHold`). |
| `sendKeys(keys)` | Надсилає клавіатурні комбінації у поточний елемент або фокус. Можна передати `Keys.ENTER`, `Keys.TAB`, або текст. |
| `keyDown(Keys.SHIFT)` | Натискає (утримує) вказану клавішу-модифікатор (Ctrl, Alt, Shift). |
| `keyUp(Keys.SHIFT)` | Відпускає клавішу-модифікатор. |
---
#### 📘 Приклади використання Actions  

```java
// Створення об’єкта Actions
Actions actions = new Actions(driver);

// Клік по елементу
actions.click(element).perform();

// Наведення курсора + клік
actions.moveToElement(menu).click().perform();

// Правий клік
actions.contextClick(element).perform();

// Подвійний клік
actions.doubleClick(element).perform();

// Drag & drop
actions.dragAndDrop(source, target).perform();
```
---
#### 🧠 Поради  
- Використовуй ланцюжки дій (actions.moveToElement(el).click().perform()) замість викликів по одному методу.
- Для перевірки hover-ефектів або drag & drop краще використовувати Actions, ніж JavaScriptExecutor.
- `.perform()` достатньо у 95% випадків, `.build()` потрібен лише для повторного використання або відкладеного запуску дій.
---

# ⌨️ 2. Клас Keys  

`Keys` використовується для симуляції натискань клавіш клавіатури у Selenium.
Його часто комбінують з `Actions` або методом `.sendKeys()`.  
---
#### 📌 Основні константи Keys

| Клавіша | Використання |
|----------|--------------|
| `Keys.ENTER` | Емуляція клавіші Enter |
| `Keys.RETURN` | Аналог Enter (різниця мінімальна) |
| `Keys.TAB` | Перехід до наступного поля |
| `Keys.ESCAPE` | Емуляція Escape |
| `Keys.BACK_SPACE` | Видалення символу назад |
| `Keys.DELETE` | Видалення символу вперед |
| `Keys.SPACE` | Пробіл |
| `Keys.ARROW_UP` | Стрілка вгору |
| `Keys.ARROW_DOWN` | Стрілка вниз |
| `Keys.ARROW_LEFT` | Стрілка вліво |
| `Keys.ARROW_RIGHT` | Стрілка вправо |
| `Keys.SHIFT` | Використовується з `keyDown()` / `keyUp()` |
| `Keys.CONTROL` | Використовується для комбінацій (наприклад, Ctrl + A) |
| `Keys.ALT` | Використовується з `keyDown()` / `keyUp()` |
| `Keys.COMMAND` | Для macOS (аналог Ctrl) |
| `Keys.F1 – Keys.F12` | Функціональні клавіші |

---
#### 📘 Приклади використання Keys
```java
// Використання Keys у sendKeys()
element.sendKeys("Hello", Keys.ENTER);

// Використання Keys у Actions
actions.keyDown(Keys.CONTROL)
       .sendKeys("a")
       .keyUp(Keys.CONTROL)
       .perform();

// Симуляція TAB для переходу між полями
element.sendKeys(Keys.TAB);

// Видалення тексту (Ctrl + A + Delete)
actions.keyDown(Keys.CONTROL)
       .sendKeys("a")
       .keyUp(Keys.CONTROL)
       .sendKeys(Keys.DELETE)
       .perform();
```
---
#### 🧠 Поради
- Використовуй Keys разом із Actions, якщо потрібно комбінувати мишу та клавіатуру в одному ланцюжку. 
- Для звичайних натискань клавіш у полі введення достатньо sendKeys().
- Для кросплатформових тестів уникай Keys.COMMAND – на Windows/Linux він не працює.
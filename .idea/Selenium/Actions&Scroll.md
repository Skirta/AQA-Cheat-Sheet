# 🖱️Скрол з використанням `Actions` 

---
У Selenium 4 додані нативні методи для прокручування сторінки без використання JavaScript.  
Клас `Actions` тепер підтримує **scroll gestures** (жести скролу мишею/тачпадом).

---

#### 📌 Основні методи для скролу

| Метод | Опис |
|------|------|
| `scrollToElement(WebElement element)` | Прокручує сторінку так, щоб обраний елемент став видимим у вікні браузера. |
| `scrollByAmount(int xOffset, int yOffset)` | Скролить відносно поточного положення на задану кількість пікселів: `xOffset` – горизонтально, `yOffset` – вертикально. |
| `scrollFromOrigin(ScrollOrigin origin, int xOffset, int yOffset)` | Скролить від заданої точки початку (`ScrollOrigin`) на вказане зміщення. Дозволяє тонкий контроль, наприклад скрол від елемента. |

---

#### ⚙️ Допоміжний клас `ScrollOrigin`
`ScrollOrigin` використовується у методі `scrollFromOrigin()` для визначення точки початку скролу.

Приклади створення:
```java
ScrollOrigin origin = ScrollOrigin.fromElement(element);         // від елемента
ScrollOrigin originWithOffset = ScrollOrigin.fromElement(element, 0, 50); // від елемента зі зміщенням
ScrollOrigin viewport = ScrollOrigin.fromViewport();             // від видимої області вікна
```
---

#### 📘 Приклади використання

---
```java
// Скрол до елемента
WebElement footer = driver.findElement(By.id("footer"));
new Actions(driver)
    .scrollToElement(footer)
    .perform();

// Скрол на певну кількість пікселів
// Скрол на 0 пікселів по горизонталі та 500 пікселів вниз
new Actions(driver)
    .scrollByAmount(0, 500)
    .perform();

//Скрол від конкретного елемента зі зміщенням
WebElement block = driver.findElement(By.id("container"));
ScrollOrigin origin = ScrollOrigin.fromElement(block);

new Actions(driver)
    .scrollFromOrigin(origin, 0, 300) // скролимо вниз на 300 пікселів від елемента
    .perform();
```
---

#### 🧠 Поради
- scrollToElement() — найзручніший метод для класичних сценаріїв (наприклад, натиснути кнопку внизу сторінки).
- Для поступового скролу використовуйте кілька викликів scrollByAmount() у циклі.
- Якщо потрібно скролити відносно конкретного елемента (наприклад, всередині контейнера з overflow), використовуйте scrollFromOrigin() з ScrollOrigin.fromElement().
- У старих версіях Selenium (<4.0) ці методи недоступні — там скрол роблять через JavascriptExecutor або moveToElement().

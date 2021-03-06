Использование
===

%v
===

Флаги
---

---
Указатели
Любое численное значение можно заменить названием переменной, начинающимся с \*, тогда будет использовано ее значение
`*currency_fractional_length`

---

a/animated
Анимирует число при любых изменениея

---

ev/event
включает прослушку эвента для данного значения

---

f()/format()
Форматирует вывод числа
`f('*[2:8].5)`

---

abs
Делает число абсолютным

---

Где
 - `'*` Символ отступа *
 - `[2:8]` максимальная(8) и минимальная(2) длина целочисленной части
 - `.5` фиксированное кол-во символов после запятой (5)

Пример

```
%v game_balance_coins f('*[2:8].*currency_fractional_length)%
%v lines f('*[:2])%
```
1. Выведет число с минимальной длиной целочисленной части `2`(И нехватку заполнит отступами `*`), максимальной `8`. Длина дробной части будет равна currency_fractional_length
2. Число с максимальной длиной 2

Class
---

`bindable` указывает парсеру что в этом элементе есть связываемое значение
`bindable_static` указывает что есть связываемое значение, но его не нужно менять при изменении переменных
`bindable fast-bind` указывает что innerHTML этого элемента полностью является c константой. Работает только со статичными значениями

%c
===

Вставляется текст в конструкцию, аналогичную переменному значению:

`%c some_text_to_translate`

# Оптимизация и ошибки

Для быстро меняющихся значений лучше проставлять bindable непосредсвенно для элемента, в котором происходит изменение:

```
//Не стоит:
<div class="bindable">
  <p>%v some_value1%</p>
  <p>%v some_value2%</p>
</div>
//Лучше
<div>
  <p class="bindable">%v some_value1%</p>
  <p class="bindable">%v some_value2%</p>
</div>
```

Для не меняющихся значений лучше наоборот использовать как можно бОльшие связки

```
<div class="bindable">
  <p>%с text1%</p>
  <p>%с text2%</p>
  <p>%с text3%</p>
  <p>%с text4%</p>
  <p>%с text5%</p>
</div>
```

## Возможные ошибки:

Можно потерять эвенты типа onclick, если бы они были повешаны на `p` из примера выше. В таком случае необходимо ставить
bindable отдельно на каждый элемент:

```
<p class="bindable fast-bind">%с text1%</p>
<p class="bindable fast-bind">%с text2%</p>
```

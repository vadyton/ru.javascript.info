Давайте пройдёмся по элементам массива:
- Для каждого элемента мы проверим, есть ли он в массиве с результатом.
- Если есть, то игнорируем его, а если нет - добавляем к результатам.

```js run demo
function unique(arr) {
  let result = [];

  for (let str of arr) {
    if (!result.includes(str)) {
      result.push(str);
    }
  }

  return result;
}

let strings = ["кришна", "кришна", "харе", "харе",
  "харе", "харе", "кришна", "кришна", ":-O"
];

alert( unique(strings) ); // кришна, харе, :-O
```

Код работает, но в нём есть потенциальная проблема с производительностью.

Метод `result.includes(str)` внутри себя обходит массив `result` и сравнивает каждый элемент с `str`, чтобы найти совпадение.

Таким образом, если `result` содержит `100` элементов и ни один не совпадает со `str`, тогда он обойдёт весь `result` и сделает ровно `100` сравнений. А если `result` большой, например, `10000`, то будет произведено `10000` сравнений.

Само по себе это не проблема, потому что движки JavaScript очень быстрые, поэтому обход `10000` элементов массива занимает считанные микросекунды.

Но мы делаем такую проверку для каждого элемента `arr` в цикле `for`.

Поэтому, если `arr.length` равен `10000`, у нас будет что-то вроде `10000*10000` = 100 миллионов сравнений. Это многовато.

Вот почему данное решение подходит только для небольших массивов.

Далее в главе <info:map-set> мы увидим, как его оптимизировать.

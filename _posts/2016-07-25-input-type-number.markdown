---
title:  "input[type='number']"
date:   2016-07-25 10:52:00
description: Избавляюсь от "спиннеров" в поле на десктопе и улучшаю на телефонах
---

Не знаю, почему, но стрелки увеличения/уменьшения значения в поле с типом number на англоязычном stackoverflow [называются](http://stackoverflow.com/questions/23372903/hide-spinner-in-input-number-firefox-29) spinner.

Тем не менее, по работе появилась хотелочка убрать стрелки с полей с типом number с десктопа и показывать цифровую клавиатуру на телефонах.

Начнем с десктопа. Здесь уберем стрелки для всех возможных браузеров:

{% highlight css %}
input[type="number"] {
  -moz-appearance: textfield /* Отключаем стрелки у FF */
}

input[type=number]::-webkit-outer-spin-button,
input[type=number]::-webkit-inner-spin-button {
    -webkit-appearance: none;
    appearance: none;
    margin: 0;
}
{% endhighlight %}

Теперь интересное: по дефолту на мобильных устройствах при выставлении у input типа number на Android'e появляется цифровая клавиатура, а на iOS - нет. Решаем это таким образом:

{% highlight html %}
<input type="number" pattern="[0-9]*" />
{% endhighlight %}

**Демо:** [http://jsbin.com/tazobel/1/edit?html,css,output](http://jsbin.com/tazobel/1/edit?html,css,output)

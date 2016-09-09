---
title:  "lodash _.sum и _.sumBy"
date:   2019-09-09 13:00:00
description: Переходим с lodash v3 на v4 и обратно
---

Вчера решил довольно простую задачку: есть массив объектов, у некоторых объектов одинаковые ключи. Нужно взять эти объекты с одинаковыми
ключами, объединить, а цифровые значения просуммировать.
Т.е. из такого:

{% highlight js %}
var data = [
  {
    alias: 'three',
    price: 100
  },
  {
    alias: 'two',
    price: 50
  },
  {
    alias: 'three',
    price: 100
  },
  {
    alias: 'three',
    price: 100
  },
  {
    alias: 'two',
    price: 50
  }
];
{% endhighlight %}

Нужно получить примерно такое: 

{% highlight js %}
[{
  alias: "three",
  val: 300
},
{
  alias: "two",
  val: 100
}]
{% endhighlight %}

Для lodash v4 все просто:

{% highlight js %}
var result = _(data)
  .map('alias')
  .uniq()
  .map(alias => ({ 
    alias: alias, 
    val: _(data).filter({ alias: alias }).sumBy('price')
  }))
  .value();
{% endhighlight %}

В lodash v3 _.sumBy нет, поэтому обходимся встроенной _.sum:

{% highlight js %}
var result = _(data)
  .map('alias')
  .uniq()
  .map(alias => ({ 
    alias: alias, 
    val: _.sum(_.pluck(_.filter(data, {alias: alias}), 'price'))
  }))
  .value();
{% endhighlight %}

## Демо

**lodash v3**

<a class="jsbin-embed" href="http://jsbin.com/kuyada/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?3.39.15"></script>

**lodash v4**

<a class="jsbin-embed" href="http://jsbin.com/kelayi/embed?js,console">JS Bin on jsbin.com</a><script src="http://static.jsbin.com/js/embed.min.js?3.39.15"></script>

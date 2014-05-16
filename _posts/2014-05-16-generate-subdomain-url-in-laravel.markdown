---
layout: post
title:  "Генерирование URL для поддоменов в Laravel"
categories: laravel
tags: laravel
---

В официальной документации данный вопрос не освещен. На самом деле все просто и логично.

Предположим у нас есть следующий роут:
{% highlight php startinline %}
Route::group(['as' => 'subdomain', 'domain' => '{account}.example.com'], function () {
    Route::get('user/{id}', function ($account, $id) {
        // do something
    });
});
{% endhighlight %}

Используя `URL::route()` мы сгенерируем нужный нам URL: 
{% highlight php startinline %}
URL::route('subdomain', ['user1', 'path1', 'param1'])
{% endhighlight %}

Вернет ссылку: `http://user1.example.com/path1?param1`

<br>
Также будет работать следующий вариант:
{% highlight php startinline %}
Route::group(['domain' => 'sub.example.com'], function () {
    Route::get('/', ['as' => 'sub.home']);
    Route::get('search/{title}', ['as' => 'sub.search']);
});

URL::route('sub.home') // => http://sub.example.com
URL::route('sub.search', ['my-title']) // => http://sub.example.com/search/my-title
{% endhighlight %}

<br>

Краткое описание [именованных роутов][doc] можно найти в официальной документации.

[doc]: http://laravel.com/docs/routing#named-routes
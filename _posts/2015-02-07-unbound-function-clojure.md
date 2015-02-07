---
layout: post
title: Clojure Unbound Function in Vim-Fireplace
date: 2015-02-07 11:31:00
published: true
---

While working through Programming Clojure, I was attempting to build a move function. After I attempted to load the code in my repl with Vim Fireplaces' `cpr` I kept getting an error when trying to call my move function `(move (create-snake))`.

{% highlight clojure %}
Attempting to call unbound fn: #'reader.snake/move
{% endhighlight %}

It turns out that the code wasn't comiling. Here was my original code:

{% highlight clojure %}
(defn move [{:keys [body dir] :as snake} & grow]
  (assoc snake :body (cons (add-points (first body) dir)
                           if grow body (butlast body))))
{% endhighlight %}

Trying to compile with vim-fireplace `cpp`

{% highlight clojure %}
java.lang.RuntimeException: Unable to resolve symbol: if in this context, compiling:(reader/snake.clj:40:22)
{% endhighlight %}

Clojure devs will probably see that I'm missing the () around my "if" form. Here's the correct code:

{% highlight clojure %}
(defn move [{:keys [body dir] :as snake} & grow]
  (assoc snake :body (cons (add-points (first body) dir)
                           (if grow body (butlast body)))))
{% endhighlight %}

It was a strang error for a person new to clojure just trying to make it through the book.

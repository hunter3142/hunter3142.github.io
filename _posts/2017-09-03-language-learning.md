---
layout: post
title: Learning a new language with my son
---
I had just finished a kata on codewars and was comparing my solution to some of the top rated solutions when my 3 year old son came up to me and asked me a question. He said "Can I have the crackers that are circles and have cheese in them like sandwiches". It may take you a second to figure out what he was asking for, as it did for me, but what he wanted was Ritz Bits. My son struggles at times with finding the right word or using the right syntax and my job is to decipher what he said and try to give him pointers so that it is easier to translate what he said the next time. 

This is very much how I feel when I'm working through katas, I get a kata to pass then I look at the top rated solutions and realize how much more elegant or concise the solution could be. So I look through the top solutions and try to store the unique methods or algorithms that are used so that I can use them next time I encounter a similar problem. Over time I've found my solutions are becoming closer and closer to the top rated solutions, just as my sons speach is becoming more and more normalized.

I'll give you a couple examples to help drive the point home. The first example is an early kata I did where you are meant to create a function that takes a string and figures out whether there are the same number of x's and o's in the string and output a boolean depending of the answer. Here was my solution in javascript:

{% highlight javascript %}
function XO(str) {
  var strLength = str.length;
  var strLowered = str.toLowerCase();
  var strArray = strLowered.split('');
  var x = 0;
  var o = 0;
  for (var i=0; i < strLength; i++) {
    if (strArray[i] == "x") {
      x += 1;
    }
    else if (strArray[i] == "o") {
      o += 1;
    }
  }
  if (x == o) {
    return true;
  }
  else if (x != o) {
    return false;
  }
}
{% endhighlight %}

Here is the top rated solution:

{% highlight javascript %}
function XO(str) {
  let x = str.match(/x/gi);
  let o = str.match(/o/gi);
  return (x && x.length) === (o && o.length);
}
{% endhighlight %}

Obviously my solution, while it worked, was overly complicated and verbose. I actually cringed as I was looking at it because of how rudimentary it is. If I had googled a bit more I probably would have found the .match() method but c'est la vie. Now to pick my ego back up a bit I'll show a more recent example where the difference between my solution and the top rated solution isn't quite so big. In this kata you create a function that takes an array, finds the integer that occurs an odd number of times, and outputs that integer. Here was my solution:

{% highlight javascript %}
function findOdd(A) {
  var obj = { };
  for (var i = 0; i < A.length; i++) {
     obj[A[i]] = (obj[A[i]] || 0) + 1;
  }
  for (var i=0; i < A.length; i++) {
    if((obj[Object.keys(obj)[i]] % 2) != 0) {
      return Number(Object.keys(obj)[i]);
    }
  }
}
{% endhighlight %}

And the top rated solution:

{% highlight javascript %}
function findOdd(A) {
  var obj = {};
  A.forEach(function(el){
    obj[el] ? obj[el]++ : obj[el] = 1;
  });
  
  for(prop in obj) {
    if(obj[prop] % 2 !== 0) return Number(prop);
  }
}
{% endhighlight %}

While the top rated solution is definitely more a little more concise, you can see that I have gotten much better at being more concise and utilizing the languages available tools more effectively. My son continues to practices english, learn more words, gain a deeper knowledge of syntax, and develop better grammer. At the same time I continue to do the same thing with a few different languages at the same time. To all those learning a new language, programming or otherwise, practice practice practice. 
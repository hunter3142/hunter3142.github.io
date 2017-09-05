---
layout: post
title: Bloccit
thumbnail-path: "img/bloccit.png"
short-description: Bloccit is a Reddit clone.

---

{:.center}
![]({{ site.baseurl }}/img/bloccit.png)

## Explanation

The point of this project was to get aquainted with some of the basics of Ruby on Rails under the guise of a basic forum site. Through Bloccit I could learn about CRUD, RESTful, user roles, associations, and routes. It also allowed me to learn more about integrating useful gems into projects.

## Problem

This was my first major Rails app so there were many new problems for me to deal with but these problems were the most interesting to me:
* Being able to "favorite" posts that you liked.
* Figuring out how to rank posts based on their popularity.
* Being able to view your site activity via your profile.

## Solution

* After adding `belongs_to` for both `:user` and `:post` in the favorites Model I used the following to create a new favorite in the favorites controller:
{% highlight ruby %}
def create
 	post = Post.find(params[:post_id])
 	favorite = current_user.favorites.build(post: post)
 	...
 }
{% endhighlight %}
* Ranking began with a voting system which used a public counter to keep track of the total votes counted for a particular post. The system take to total number of upvotes (+1) and the total number of downvotes (-1) and displays the posts popularity as an integer.
* Profile setup familiarized me with Rails `render`
{% highlight javascript %}
<%= render @user.posts %>
{% endhighlight %}
and `pluralize`
{% highlight javascript %}
<%= pluralize(@user.posts.count, 'post') %>
{% endhighlight %}
Which takes a number as the first argument, in this case the number of posts a user has, and a word as the second argument and displays the proper form of the given word. The code behind this method is pretty fascinating and I recommend taking a look at it if you get a chance.

## Conclusion

Learning routes was an eye opening experience when is comes to the anatomy of URLs and what kinds of information a URL can give the user. While Rails is an amazing framework which definitely helps streamline the building process, that streamlining can lead to some added confusion when problems arise. On multiple occassions I found myself having to do some research into the "magic" rails was performing so that I could fix bugs and errors. Some people may see this as a downside to Rails but I actually liked the process of getting frustrated with an error followed by the feeling of accomplishment when I finally figured out what was really going on. 

---
layout: post
title: Blocipedia
thumbnail-path: "img/blocipedia.png"
short-description: A Wikipedia clone with a paid premium membership option.

---

{:.center}
![]({{ site.baseurl }}/img/blocipedia.png)

## Explanation

This build was meant to solidify and expand on some of the skills that I learned during the Bloccit project. It also gave me a chance to get used to implementing different types of gems into a project. With Blocipedia the user is able to purchase an upgraded "Premium" account which allows you to create private wikis and assign collaborators to private wikis. 

## Problem

There were a couple of hurdles that I had to overcome in order to implement certain user stories. One such hurdle involved what happens to a Premium users private wikis if they downgrade their account. The other issue was figuring out how to allow a creator of a private wiki to assign collaborators for that wiki from among the apps users. 

## Solution

For the issue of how to properly downgrade a Premium user to a Standard membership the solution actually ended up being quite simple and elegent. If you remove the notices from the method downgrading to a Standard membership looks like this:
{% highlight ruby %}
def downgrade_to_standard
    if current_user.premium? && current_user.standard!
      current_user.wikis.where(private: true).update_all(private: false)
      ...
{% endhighlight %}
The `If` statement checks whether the user is a Premium member, otherwise they would not be able to downgrade, then it changes the users role to Standard. Within the `If` statement we check all of the users wikis to see which are set to private then change them to public wikis.

The solution for creating collaborators was a little more painstaking. In order to assign a collaborator to a private wiki you have to have checks along the way to make sure that the current user is a Premium user, that the wiki `belongs_to` the current users, and that the collaborator is an actual user. If all of these ducks are in a row the following code is run when you add a colaborator to a wiki:
{% highlight ruby %}
@collaborator = Collaborator.new(wiki_id: @wiki.id, user_id: params[:user_id])
{% endhighlight %}
This makes it so that the collaborator `belongs_to` the wiki and associates the collaborators user id with the wiki id, creating a Has Many Through relationship. Once this is set up you have to go through the scopes to add an additional statement which allows users to view or edit private wikis if they are assigned as a collaborator. 

## Conclusion

While I really enjoyed learning about new data relationships I think what I enjoyed most was seeing how intersting and powerful Ruby Gems can be. It seems like it would be easy to go overboard with Gems and bloat a project with a lot of unnecessary methods and features but if used judiciously they can be a real asset.

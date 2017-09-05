---
layout: post
title: Bloc Jams
thumbnail-path: "img/blocjams.png"
short-description: BlocJams is a Spotify replica for playing all of your favorite music.

---

{:.center}
![]({{ site.baseurl }}/img/blocjams.png)

## Explanation

The plan for this project was to build a sleek music app with full functionality and, most importantly, no ads. The design elements were developed by Bloc and it was my responsibility to utilize those elements while building a seamless music app. The songs were provided by Bloc as well, my task was to set up the code resposible for accessing and displaying the music database.

## Problem

There were a couple interesting problems that needed to be addressed during this project:
* Ensuring that the site was responsive and optimized for mobile devices and computers alike.
* Creating a seek/progress slider for the player bar that updates in real time.

## Solution

* Responsiveness was achieved using basic media queries like these:
{% highlight javascript %}
@media (min-width: 640px) {
	.column {
     	float: left;
     	padding-left: 1rem;
     	padding-right: 1rem;
 	}
}
@media (min-width: 1024px) {
	html { font-size: 120%; }
}
{% endhighlight %}

* The most important parts of the seekbars functionality are the following bits of code:
{% highlight javascript %}
var notifyOnChange = function(newValue) {
	if (typeof scope.onChange === 'function') {
		scope.onChange({value: newValue});
	}
};
{% endhighlight %}
<p style="text-align: center;">This keeps track of any changes made to the location of the seek slider.</p>

{% highlight javascript %}
var calculatePercent = function(seekBar, event) {
	var offsetX = event.pageX - seekBar.offset().left;
	var seekBarWidth = seekBar.width();
	var offsetXPercent = offsetX / seekBarWidth;
	offsetXPercent = Math.max(0, offsetXPercent);
	offsetXPercent = Math.min(1, offsetXPercent);
	return offsetXPercent;
};
{% endhighlight %}
<p style="text-align: center;">This section determines how far the seek slider is offset from the left side of the seek bar, turns this into a percentage, then we can apply this percentage to the length of the song to determine which part of the song should be playing.</p>

## Conclusion

This site was a great way to test my AngularJS skills. The framework is pretty robust and though there are features I did not use in this project, it was a good introduction into just how effective using a javascript framework can be. Future iterations could include creating playlists, favoriting songs/albums, or sharing playlists with other users. 

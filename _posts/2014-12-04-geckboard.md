---
layout: post
titile: Geckoboard
---

Today I&#39;ve been looking at geckoboard once more.   
I looked at it a while back.  
I also met some of the team at the [silicon milkroundabout 6.0](https://www.siliconmilkroundabout.com).  
I got a free (purple) T-shirt then, maybe very happy :)  

So looking back at it now, I didn&#39;t expect [so many services](https://www.geckoboard.com/integrations/).  
Maybe I just didn&#39;t noticed them before, maybe I just wasn&#39;t interrested enought, I don&#39;t know.  
I was particulary keen to see google analytics as I use it for my [dad&#39;s online](http://guiro.org) [presence's](http://guiro.bzh) analytics.  
So far it has been a treat.  
I can do a clutter free, login free, simple dashboard.  
With a bit of [DNS wizzardry](https://geckoboard.zendesk.com/hc/en-us/articles/202136903-Custom-domain-names) I could even get to dashboard with a simple URL.  

I&#39;m not using it massivelly, just enought to give some vanity metrics to my dad.  
Basically I was using what Google Analytics provided.
I got an email delivered every morning(ish) to both of us.  
The good thing is my dad like email, the bad thing is that I already have [enought emails](http://theoatmeal.com/comics/email_monster).  
Plus I have it delivered as two pdf with is not really great eaither.  
The other way is to use the builtin dashboard.  
I don&#39;t particulary want to log in and drill down into google analytics, life is too short for that.  
Also the formating was not of my liking.  
So overall, not a great experience.    

I had a good idea of what I needed, sessions over different time scale, page view and time per page, country of origin.  
Then, I need to be able to remove bouncing traffic.  
So i went on my merry way, and did the dashboard.  
Once there, I remmembered it was general availability for dommain names in [.bzh](http://www.pik.bzh/).  
Now I needed another dashboard, well the same one with a different target in my google analytics.  
It was easy to clone the dashboard, but then it was a bit tiresome to go to each widget and change the target.  
It could be configurable per dashboard.  
Of course that would require more settings, more UI clutter etc.  
Maybe an advance mode to be able to do batch, or maybe over an API for those who need it.  
Well not that anoying in the end (just time consuming).  

There is a page that help with [Google Analytics](https://www.geckoboard.com/learn/help-and-support/how-to-guides/google-analytics-and-filters).
It also link to a pdf, where you learn dashboard 101.  
This page details operators, dimensions and metrics one can use to create a filter.  
It also provides definition of the available widget.  
It is well made and insightfull.  

I think that&#39;s being a company help to provide educational material.  
Most of the open source project don&#39;t even have a place holder for that.  
There is often documentation, but it mostly revolve around technical details like implementation details, installation and operations advice.  
This is why confereces and talks are an essential part of open source in general.  
So open source dashboard will not come with a huge amount of materials, but you can find it.
You probably will also get to know the source of the knowlegde, like which video to watch, which book to read to go further into knowledge etc.
That s how I got to read Information Dashboard Design by Stephen Few.  

Overall I think Geckboard does a very good job at explaining workflow too.  
At the begining you put everything you can (the same way you "log all the things").
Then you try to make sense of it.
You realise it is cluttered and make some cleaning.
Finally you revisit your dashboard often so they remain relevant.

They also are of good advice.
They recomend that you split your dashboard by audiance.
Your boss and the boss of your boss don't have the same need.
Also the dashboard type can be different.
The dashboard to check if your service are up and running are hopefully not the same one you look at when you try to undertand what your customer are like today.
It's well explain in a neat [6 rules set](https://www.geckoboard.com/blog/building-great-dashboards-6-golden-rules-to-successful-dashboard-design/)


You can also do custom graphs with geckoboard.  
One of them is my favorite one in the whole world the [bullet-graph](https://developer.geckoboard.com/#bullet-graph).  
While I think the name is wrong, this type of graph provides some of the most condenced informaton rich graph ever.  
This is from [wikipedia](http://en.wikipedia.org/wiki/Bullet_graph):
"The bullet graph features a single, primary measure (for example, current year-to-date revenue), compares that measure to one or more other measures to enrich its meaning (for example, compared to a target), and displays it in the context of qualitative ranges of performance, such as poor, satisfactory, and good. The qualitative ranges are displayed as varying intensities of a single hue to make them discernible by those who are color blind and to restrict the use of colors on the dashboard to a minimum."  

I have no use for the ranges under the bullet graph bar in my dashbaord, hence I didn&#39;t use it.  
I don&#39;t have conversion goals or expectation out of page views/sessions etc.  
Still it is available and that can only noted as a good understanding power a dashboard can provide.  
On the other side, the Geck-o-Meter, a [Tachometer](http://en.wikipedia.org/wiki/Tachometer) is also available.  
And unless they are many people displaying speed with Geckoboard, it&#39;s probably not for the best.  
Actually same goes for pie chart, they are bad and should be banned.  
Any kind of bar or sparkline would do the same job, with more data in a smaller space.  
If you are not sure why you don&#39;t want to waste space, watch this talk by [Jarkko Laine](http://vimeo.com/75318590).  
Actually go watch all the video from [monitorama](http://monitorama.com/) and [monitorama.eu](http://monitorama.eu/).  

Finally I looked at polling data from APIs.
So far I find it quite limiting.  
Geckoboard expect you to create an API, and you to pull from it.
Not say poll from github or the other people that you depend on and graph that.  
They actually expect 'Items' like [in this exemple](https://developer.geckoboard.com/#text):

{% highlight js %}
{
  "item": [
    {
      "text": "Unfortunately, as you probably already know, people",
      "type": 0
    },
    {
      "text": "As you might know, I am a full time Internet",
      "type": 1
    }
  ]
}
{% endhighlight js %}

It means that if you want to consume say, [github api](https://status.github.com/api):
{% highlight js %}
{
  "status": "good",
  "last_updated": "2012-12-07T18:11:55Z"
}
{% endhighlight js %}

I also checked the push options for widget.  
I found an [sinatra app](https://github.com/geckoboard/push-sinatra-example) on the geckboard twiter.  
I even made a [pull request](https://github.com/geckoboard/push-sinatra-example/pull/1) because the link to the documentation was now outdated.  
That done I also added a bit more information about where to get the API and Widget key.  
Finally I uploaded the code to [openshift](https://www.openshift.com/).  
Here it is, a [geckoboard push api tester](http://geckoboard-kyzh.rhcloud.com/).  

What is missing ?
* A way to do snapshot (to come back to a previous state)
* commit messages (as in git commit message) when you do change the dashboard.
* Tooltips: it is definitly missing to give more understanding of the data. Especially to explain the secondary number (one might no know the period the primary number is compared to)
* The possibility to fiddle with the api polling results.
* A middle price tag for individual with more than 1 dashboard, but say less than 60 quid a month to spend on a rather nice dashboard.  

There are [alternatives](http://alternativeto.net/software/geckoboard/).  
One of my favorite one is [dashing](http://dashing.io/) if you have the possibility to run it by yourself.  
If you like geckboard and would like 10% off, you can always use [this link](http://ssqt.co/bSEX).  


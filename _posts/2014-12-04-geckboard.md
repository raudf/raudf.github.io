---
layout: post
titile: Geckoboard
---

Today I&#39;ve been looking at geckoboard once more.   
I looked at it a while back.  
I also met some of the team at the [silicon milkroundabout 6.0](https://www.siliconmilkroundabout.com).  
I got a free (purple) T-shirt then, maybe very happy :)  

So looking back at it now, I didn&#39;t expect [so many services](https://www.geckoboard.com/integrations/).  
Maybe I just didn&#39;t noticed before, maybe I just wasn&#39;t interrested enought, I don&#39;t know.  
I was particulary keen to see google analytics as I use it for my [dad&#39;s online](http://guiro.org) [presence](http://guiro.bzh) analytics.  
So far it has been a treat.  
I can do a clutter free, login free, simple dashboard.  
With a bit of [DNS wizzardry](https://geckoboard.zendesk.com/hc/en-us/articles/202136903-Custom-domain-names) I could even get to dashboard with a simple URL.  

I&#39;m not using it massivelly, just enought to give some vanity metrics to my dad.  
Basically I was using what Google Analytics provided.
I got an email delivered every morning(ish) to both of us.  
The good thing is my dad like email, the bad thing is that I already have [enought emails](http://theoatmeal.com/comics/email_monster).  
The other way is to use the builtin dashboard.  
I don&#39;t particulary want to log in and drill down into google analytics, life is too short for that.  
Also the formating was not of my liking.  
So overall, not a great experience.    

I had a good idea of what I needed, sessions over different time scale, page view and time per page, country of origin.  
Then, I need to be able to remove bouncing traffic.  
So i went on my merry way, and did the dashboard.  
Once there, I remmember it was general availability for dommain name in .bzh.  
Now I needed another dashboard, well the same one with a different target in my google analytics.  
It was easy to clone the dashboard, then  it was a bit tiresome to go to each widget and change the target.  
It could be configurable per dashboard, but would require more settings, more UI clutter etc.  
Maybe an advance mode to be able to do batch, or maybe over the API.  
Well not that anoying, just time consuming.  

There is a page that help with [Google Analytics](https://www.geckoboard.com/learn/help-and-support/how-to-guides/google-analytics-and-filters).
It also link to a pdf, where you learn dashboard 101.  
This page details operators, dimensions and metrics one can use to create a filter.  
It also provides definition of the available widget.  
It is well made and insightfull.  
I think that&#39;s being a company help to provide educational material.  
Most of the open source project don&#39;t even have a place holder for that.  
There is often documentation, but it mostly revoilve around technical details like implementation details, installation and operations advice.  
This is why confereces and talks are an essential part of open source in general.  
So open source dashboard will not come with a huge amount of materials, but you can find it.
You probably will also get to know the source of the knowlegde, like which video to watch, which book to go further into knowledge etc.
That s how I got to read Information Dashboard Design by Stephen Few.  
Maybe you get to know less of where the good pratice come from and how to get more knowledge sources.

Overall I think Geckboard does a very good job at explaining work flow too.  
At the begining you put everything you can (the same way you "log all the things").
Then 

You can also do custom graphs.  
One of them is my favorite one in the whole world the [bullet-graph](https://developer.geckoboard.com/#bullet-graph).  
While I think the name is wrong, this type of graph provides some of the most condenced informaton rich graph ever.  
This is from [wikipedia](http://en.wikipedia.org/wiki/Bullet_graph):
"The bullet graph features a single, primary measure (for example, current year-to-date revenue), compares that measure to one or more other measures to enrich its meaning (for example, compared to a target), and displays it in the context of qualitative ranges of performance, such as poor, satisfactory, and good. The qualitative ranges are displayed as varying intensities of a single hue to make them discernible by those who are color blind and to restrict the use of colors on the dashboard to a minimum."  
I don&#39;t have conversion goals or expectation out of page views/sessions etc.  
For those 2 dashboard, I have no use for the ranges under the bullet graph bar, hence I didn&#39;t use it.
Still it is available and that can only noted as a good understanding of dashboard from teh Geckobaord team.  
On the other side, the Geck-o-Meter, a [Tachometer](http://en.wikipedia.org/wiki/Tachometer) is also available.  
And unless they are many people displaying speed with Geckoboard, it&#39;s probably not for the best.  
Any kind of bar or sparkline would do the same job, with more data in a smaller space.  
If you are not sure why you don&#39;t want to waste space, watch this talk by [Jarkko Laine](http://vimeo.com/75318590).  
Actually go watch all the video from [monitorama](http://monitorama.com/) and [monitorama.eu](http://monitorama.eu/).  
Actually same goes for pie chart, they are bad and should be banned.  


I also looked at polling data from APIs.
So far I fint it quite limiting.  
Geckoboard expect you to create an API, and you to pull from it, not say poll from github or the other people that you depend on.  
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
That done i also added a bit more information about where to get the API and Widget key.  
Finally I uploaded the code to [openshift](https://www.openshift.com/).  
Here it is, a [geckoboard push api tester](http://geckoboard-kyzh.rhcloud.com/).  

What is missing ?
* A way to do snapshot and commit messages (as in git commit message) when you do 
* Tooltip: it is definitly missing to give more understanding of the data. Especially to explain the secondary number (one might no know the period the primary number is compared to)
* The inability to fiddle with the api polling results.
* A middle price tag for individual with more than 1 dashboard, but say less than 60 quid a month to spend on a rather nice dashboard.  

If you like geckboard and would like 10% off, you can always use [this link](http://ssqt.co/bSEX)

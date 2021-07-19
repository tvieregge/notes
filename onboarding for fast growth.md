source: https://lethain.com/productivity-in-the-age-of-hypergrowth/

need to get ahead of growth, or you'll always be behind, especially since [[good processes is eveolved, not designed]]
    
> if you’re doubling every six months and it takes six to twelve months to ramp up, then you can quickly find a scenario where untrained engineers increasing outnumber the trained engineers
>
> ![growth|500](https://lethain.com/static/blog/2016/training.png)
 
 The process for hiring+onboadring looks like this
![embed](https://lethain.com/static/blog/2016/training_loop.png)

Let's look at where the time sinks are. For the setup, lets make a few assumptions
- it takes 6 months to train an engineer
- untrained engineers are 1/3 as productive
- training takes 10 h/week (0.25 of total work) of a trained engineers time
- the ratio of trained to untrained is $2:1$
    - we'll do the exercies with 1x as well, more relevant for [[voltus]]

This makes total productivity for the three people $$2*0.33+(1-2*0.25)=1.16$$ $$1.16/3 ~= 0.37$$ And with a $1:1$ ratio $$1*0.33+(1-1*0.25)=1.08$$ $$1.08/2 = 0.54$$

But if we add in time spent hiring and assume
- 20% of interviewed candidates join
- 4 interview per candidate
- 2 hours total time per interview (prep+interview+debrief)
- only trained engineers interview
- double in 6 months

Each trained engineer does $1/0.2 * 4=20$ interviews -> 40 hours interviewing over the doubling period (~1.7h/week). Not bad if that's spread over the whole team, but if only the trained engineers are interviewing (and 50 are trained, because we just doubled) the it's really $1.7*2=3.3$ hours.

Adding that into our earlier efficiency formula $$0.33+(1-0.25-3.3/40)=0.9975$$ $$1.08/2 = 0.49$$

Less than half an engineer's productivity out of two people for *6 moths* :(

But what if it took 1 month to train someone?
- the ratio of trained to untrained would be more like $4:1$ (depending on what part of the doubling we're at)
- almost eveyone is trained, reducing the interviewing workload to ~2h/week

So the untrained engineer, plus the one training them, plus the 3 other engineers gives us
$$0.33+(1-0.25-2/40)+3*(1-2/40)=3.88$$ $$3.88/4 = 0.97$$ *Much* better
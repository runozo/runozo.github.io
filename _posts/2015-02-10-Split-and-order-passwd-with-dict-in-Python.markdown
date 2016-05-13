---
layout: post
title:  "Split and order /etc/passwd file with a dict in Python"
date:   2015-02-10 16:12:20
categories: python quiz
---
Here I have another quiz from the newsletter mentioned [here]({% post_url 2015-01-08-Get-last-line-of-a-text-file-in-Python %}):

*"From the file /etc/passwd you must print out a dict sorted by key. The key of dict is field #1 and the value is field #3 of the passwd file. The lines beginning with # must be threated as comments."*

Seems not so hard, let's propose this:

{% highlight python %}
d = dict([(line.split(':')[0], line.split(':')[2])
          for line in open('/etc/passwd').readlines() if not line.startswith('#')])
for k, v in sorted(d.items()):
    print(k, v)
{% endhighlight %}

This time I tried to keep it as shorter as possible using the beloved Python [listing comprehension](https://docs.python.org/2/tutorial/datastructures.html#list-comprehensions), then converting the list to a dictionary with [dict()](https://docs.python.org/2/library/stdtypes.html#mapping-types-dict). Let's see which were the proposed answers, instead.

One plain version:

{% highlight python %}
users = {}
with open('/etc/passwd') as f:
    for line in f:
        if not line.startswith("#"):
            user_info = line.split(":")
            users[user_info[0]] = user_info[2]

for username in sorted(users):
    print("{}:{}".format(username, users[username]))
{% endhighlight %}

and one with dictionary comprehension:

{% highlight python %}
users =  { line.split(':')[0] : line.split(':')[2]
           for line in open('/etc/passwd')
           if not line.startswith('#') }
for username in sorted(users):
    print("{}:{}".format(username, users[username]))
{% endhighlight %}

This time, this last is very close to mine solution that instead is more old style. Which is the fastest one, then?
I ran both of them on my Linux box with `perf stat -r 100`.
Mine scores: `0,015599686 seconds` and his: `0,015344643 seconds`
As one would expect is almost identical scores.

So close!


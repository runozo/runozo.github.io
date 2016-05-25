---
layout: post
title:  "Get last line of a text file with Python"
date:   2015-01-08 16:23:20
categories: python quiz
---
I subscribed myself to a newsletter that propose each week a new [Python](http://www.python.org "Python language web site") quiz, then answer it the day after.
I accepted the challenge (for now, at least) and answer here when I've a solution to the quizzes.
Let's start with the first post with the first quiz.

The first question was:

*"Ask the user for the name of a text file. Display the final line of that file."*

Seems quietly easy, here is my solution. I don't like the fact I needed to "import sys" but didn't find nothing better for asking a filename to user.

{% highlight python %}
import sys
try:
    with open(sys.argv[1], 'r') as f:
        row = old_row = f.readline()
        while row:
            old_row = row
            row = f.readline()
        print("Last line is: \n\n%s\n" % old_row)
except:
    print("Use like this:\n%s <path_to_file>\n" % sys.argv[0])
{% endhighlight %}

This instead was the "correct" answer:
{% highlight python %}
filename = raw_input("Enter a filename: ")
print(open(filename).readlines()[-1])
{% endhighlight %}

Ok, first quiz and first interpretation error here. I wonder myself which part of "Ask the user" was not clear to me :-). My solution needs the filename passed as command line argument, and doesn't ask the user for it. Next time I'll try to understand better the posed question.

See ya!


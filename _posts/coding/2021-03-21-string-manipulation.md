---
layout: post
title: "String Manipulation"
date: 2020-03-21 00:00:00 -0000
categories: coding 
---

The coding challenges below were provided on [HackerRank](https://www.hackerrank.com/interview/interview-preparation-kit/strings/challenges).  
<br>
<hr>
<br>
Challenge: Making Anagrams 

Problem Statement: Given two strings, _a_ and _b_, that may or may not be of the same length, determine the minimum number of character deletions required to make _a_ and  _b_ anagrams. Any characters can be deleted from either of the strings.

{% highlight python %}

def makeAnagram(a, b):
    # delCount represents the final result
    # number of counts that needs to be deleted.
    delCount = 0
    commonLst = [] 
    # This part is to find out the characters 
    # present in string a but not in string b, and vice versa.
    diffLstA = [x for x in a if x not in b]
    diffLstB = [x for x in b if x not in a]
    # If there is a character that appears in both strings, 
    # we shall determine how many times it occurs in each of the string, 
    # thus determine the difference.
    for char in a:
        if char in b and char not in commonLst:
            aCount = a.count(char)
            bCount = b.count(char)
            commonLst.append(char)
            if aCount != bCount:
                delCount += abs(aCount - bCount)    
    # Sum up the result from the previous two circumstances.                 
    delCount += len(diffLstA) + len(diffLstB);
    return delCount;

{% endhighlight %}
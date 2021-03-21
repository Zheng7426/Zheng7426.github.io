---
layout: post
title: "String Manipulation"
date: 2021-03-21 00:00:00 -0000
categories: coding 
---

The coding challenges below were provided by [HackerRank](https://www.hackerrank.com/interview/interview-preparation-kit/strings/challenges).  
<br>
<hr>
<br>

### Challenge: Making Anagrams 

Given two strings, _a_ and _b_, that may or may not be of the same length, determine the minimum number of character deletions required to make _a_ and  _b_ anagrams. Any characters can be deleted from either of the strings.

```python

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

```

<br>

### Challenge: Sherlock and the Valid String

Sherlock considers a string to be valid if all characters of the string appear the same number of times. It is also valid if he can remove just 1 character at 1 index in the string, and the remaining characters will occur the same number of times. Given a string _s_, determine if it is valid. If so, return <code>YES</code>, otherwise return <code>NO</code>.


```python

def isValid(s):
    # Generate a dictionary that captures 
    # the occurrences of each character
    seen = {}
    for char in s:
        if char not in seen:
            seen[char] = 1
        else:
            seen[char] += 1
    # Turning the resulting 
    # dictionary values into a proper list
    dictVal = list(seen.values())
    # Obtain the maximum and minimum values
    high = max(dictVal)
    low = min(dictVal)
    maxFrequency = 0
    majorNum = 0
    # Find out which value makes up the majority
    for i in dictVal:
        currFrequency = dictVal.count(i)
        if currFrequency > maxFrequency:
            maxFrequency = currFrequency
            majorNum = i 
    # What we are interested is whether the 
    minorLst = [x for x in dictVal if x != majorNum]
    # If the difference between major number
    # and minor number exceeds 1, 
    # then removing one occurrence is simply not enough
    if high - low > 1 and minorLst[0] != 1:
        return "NO"
    # Check to see if there are more than one minor numbers present
    if len(minorLst) > 1:
        return "NO"
    return "YES"
  
```
---
title: Playing around with Python
date: '2013-08-22T12:30:00.000+02:00'
search: true
author: Hermann Lotter
comments: true
tags:
- sql
published: true
---

So I've been looking for a creative outlet for this very busy brain of mine, 
and TSQL doesn't seem to fit the bill so much. I looked into Java and Python 
and seeing that Python is an interpreted language, I've decided to give it a 
go. 

And it seemed only fair that one of the first things I did with it was 
weightlifting related. One of the beginning chapters discussed mostly 
mathematical equations and all I could think of was how many plates should be 
on the bar. 

Here’s what I did, and I’m pretty sure there’s easier ways to this, but this 
is what I have and lank proud of it. 
<code style="font-size: 12px;"><span style="color: black;"> 
<span style="color: green;"># setup<span style="color: black;">measure <span 
style="color: blue;">= <span style="color: darkred;">'kg' <span style="color: 
green;"># use kg or lbs<span style="color: black;">increment <span 
style="color: blue;">= <span style="color: black;">2.5 <span style="color: 
green;"># round to the nearest<span style="color: black;">barweight <span 
style="color: blue;">= <span style="color: black;">20.0 
<span style="color: green;"># enter the desired weight on the bar<span 
style="color: black;">weigth <span style="color: blue;">= <span style="color: 
black;">eval<span style="color: grey;">(<span style="color: black;">input<span 
style="color: grey;">(<span style="color: darkred;">'Enter the weight: '<span 
style="color: grey;">)) 
<span style="color: green;"># rounded weight<span style="color: black;">weight 
<span style="color: blue;">= <span style="color: black;">increment <span 
style="color: grey;">* <span style="color: black;">round<span style="color: 
grey;">(<span style="color: black;">weigth <span style="color: grey;">/ <span 
style="color: black;">increment<span style="color: grey;">) 
<span style="color: green;"># weight without the bar<span style="color: 
black;">weightwobar <span style="color: blue;">= <span style="color: 
black;">weight <span style="color: grey;">- <span style="color: 
black;">barweight 
<span style="color: green;"># weight on one side of the bar<span style="color: 
black;">weightoneside <span style="color: blue;">= <span style="color: 
black;">weightwobar <span style="color: grey;">/ <span style="color: black;">2 
remainingWeight <span style="color: blue;">= <span style="color: 
black;">weightoneside 
<span style="color: green;"># number of 20's<span style="color: 
black;">numberOf20 <span style="color: blue;">= <span style="color: 
black;">int<span style="color: grey;">(<span style="color: 
black;">remainingWeight <span style="color: grey;">// <span style="color: 
black;">20<span style="color: grey;">)<span style="color: 
black;">remainingWeight <span style="color: blue;">= <span style="color: 
black;">remainingWeight <span style="color: grey;">% <span style="color: 
black;">20 
<span style="color: green;"># number of 15's<span style="color: 
black;">numberOf15 <span style="color: blue;">= <span style="color: 
black;">int<span style="color: grey;">(<span style="color: 
black;">remainingWeight <span style="color: grey;">// <span style="color: 
black;">15<span style="color: grey;">)<span style="color: 
black;">remainingWeight <span style="color: blue;">= <span style="color: 
black;">remainingWeight <span style="color: grey;">% <span style="color: 
black;">15 
<span style="color: green;"># number of 10's<span style="color: 
black;">numberOf10 <span style="color: blue;">= <span style="color: 
black;">int<span style="color: grey;">(<span style="color: 
black;">remainingWeight <span style="color: grey;">// <span style="color: 
black;">10<span style="color: grey;">)<span style="color: 
black;">remainingWeight <span style="color: blue;">= <span style="color: 
black;">remainingWeight <span style="color: grey;">% <span style="color: 
black;">10 
<span style="color: green;"># number of 5's<span style="color: 
black;">numberOf5 <span style="color: blue;">= <span style="color: 
black;">int<span style="color: grey;">(<span style="color: 
black;">remainingWeight <span style="color: grey;">// <span style="color: 
black;">5<span style="color: grey;">)<span style="color: 
black;">remainingWeight <span style="color: blue;">= <span style="color: 
black;">remainingWeight <span style="color: grey;">% <span style="color: 
black;">5 
<span style="color: green;"># number of 2.5's<span style="color: 
black;">numberOf2and5 <span style="color: blue;">= <span style="color: 
black;">int<span style="color: grey;">(<span style="color: 
black;">remainingWeight <span style="color: grey;">// <span style="color: 
black;">2.5<span style="color: grey;">)<span style="color: 
black;">remainingWeight <span style="color: blue;">= <span style="color: 
black;">remainingWeight <span style="color: grey;">% <span style="color: 
black;">2.5 
<span style="color: green;"># number of 1.25's<span style="color: 
black;">numberOf1and25 <span style="color: blue;">= <span style="color: 
black;">int<span style="color: grey;">(<span style="color: 
black;">remainingWeight <span style="color: grey;">// <span style="color: 
black;">1.25<span style="color: grey;">)<span style="color: 
black;">remainingWeight <span style="color: blue;">= <span style="color: 
black;">remainingWeight <span style="color: grey;">% <span style="color: 
black;">1.25 
<span style="color: green;"># Display the results<span style="color: 
blue;">print<span style="color: grey;">(<span style="color: darkred;">'Your 
weight'<span style="color: grey;">, <span style="color: black;">weigth<span 
style="color: grey;">, <span style="color: black;">measure<span style="color: 
grey;">, <span style="color: darkred;">'( rounded to the closest'<span 
style="color: grey;">, <span style="color: black;">increment<span 
style="color: grey;">, <span style="color: black;">measure<span style="color: 
grey;">, <span style="color: darkred;">'='<span style="color: grey;">, <span 
style="color: black;">weight<span style="color: grey;">, <span style="color: 
black;">measure<span style="color: grey;">,<span style="color: darkred;">') 
consists ofn'<span style="color: grey;">,<span style="color: darkred;">'n' 
't'<span style="color: grey;">, <span style="color: black;">numberOf20<span 
style="color: grey;">, <span style="color: darkred;">'x 20kg plates'<span 
style="color: grey;">, <span style="color: darkred;">' ='<span style="color: 
grey;">, <span style="color: black;">numberOf20 <span style="color: grey;">* 
<span style="color: black;">20<span style="color: grey;">, <span style="color: 
black;">measure<span style="color: grey;">,<span style="color: 
darkred;">'n'<span style="color: grey;">,<span style="color: 
darkred;">'t'<span style="color: grey;">, <span style="color: 
black;">numberOf15<span style="color: grey;">, <span style="color: 
darkred;">'x 15kg plates'<span style="color: grey;">, <span style="color: 
darkred;">' ='<span style="color: grey;">, <span style="color: 
black;">numberOf15 <span style="color: grey;">* <span style="color: 
black;">15<span style="color: grey;">, <span style="color: 
black;">measure<span style="color: grey;">,<span style="color: 
darkred;">'n'<span style="color: grey;">,<span style="color: 
darkred;">'t'<span style="color: grey;">, <span style="color: 
black;">numberOf10<span style="color: grey;">, <span style="color: 
darkred;">'x 10kg plates'<span style="color: grey;">, <span style="color: 
darkred;">' ='<span style="color: grey;">, <span style="color: 
black;">numberOf10 <span style="color: grey;">* <span style="color: 
black;">10<span style="color: grey;">, <span style="color: 
black;">measure<span style="color: grey;">,<span style="color: 
darkred;">'n'<span style="color: grey;">,<span style="color: 
darkred;">'t'<span style="color: grey;">, <span style="color: 
black;">numberOf5<span style="color: grey;">, <span style="color: darkred;">'x 
5kg plates'<span style="color: grey;">, <span style="color: darkred;">' 
='<span style="color: grey;">, <span style="color: black;">numberOf5 <span 
style="color: grey;">* <span style="color: black;">5<span style="color: 
grey;">, <span style="color: black;">measure<span style="color: grey;">,<span 
style="color: darkred;">'n'<span style="color: grey;">,<span style="color: 
darkred;">'t'<span style="color: grey;">, <span style="color: 
black;">numberOf2and5<span style="color: grey;">, <span style="color: 
darkred;">'x 2.5kg plates'<span style="color: grey;">, <span style="color: 
darkred;">' ='<span style="color: grey;">, <span style="color: 
black;">numberOf2and5 <span style="color: grey;">* <span style="color: 
black;">2.5<span style="color: grey;">, <span style="color: 
black;">measure<span style="color: grey;">,<span style="color: 
darkred;">'n'<span style="color: grey;">,<span style="color: 
darkred;">'t'<span style="color: grey;">, <span style="color: 
black;">numberOf1and25<span style="color: grey;">, <span style="color: 
darkred;">'x 1.25kg plates'<span style="color: grey;">, <span style="color: 
darkred;">' ='<span style="color: grey;">, <span style="color: 
black;">numberOf1and25 <span style="color: grey;">* <span style="color: 
black;">1.25<span style="color: grey;">, <span style="color: 
black;">measure<span style="color: grey;">,<span style="color: 
darkred;">'n'<span style="color: grey;">,<span style="color: 
darkred;">'t'<span style="color: grey;">, <span style="color: darkred;">' 
'<span style="color: grey;">, (<span style="color: black;">numberOf20 <span 
style="color: grey;">* <span style="color: black;">20<span style="color: 
grey;">)+(<span style="color: black;">numberOf15 <span style="color: grey;">* 
<span style="color: black;">15<span style="color: grey;">)+(<span 
style="color: black;">numberOf10 <span style="color: grey;">* <span 
style="color: black;">10<span style="color: grey;">)+(<span style="color: 
black;">numberOf5 <span style="color: grey;">* <span style="color: 
black;">5<span style="color: grey;">)+(<span style="color: 
black;">numberOf2and5 <span style="color: grey;">* <span style="color: 
black;">2.5<span style="color: grey;">)+(<span style="color: 
black;">numberOf1and25 <span style="color: grey;">* <span style="color: 
black;">1.25<span style="color: grey;">), <span style="color: 
black;">measure<span style="color: grey;">, <span style="color: 
darkred;">'n'<span style="color: grey;">, 
)</code> 
This prompts one for the amount of weight and will then output the individual 
plates required. 

<div class="separator" style="clear: both; text-align: center;">[<img 
border="0" 
src="http://1.bp.blogspot.com/-1ZrLtmu6kJo/VHFtU9XT9EI/AAAAAAABF-M/QL1q6Cgld6Y/s1600/python.png" 
height="193" width="640" 
/>](http://1.bp.blogspot.com/-1ZrLtmu6kJo/VHFtU9XT9EI/AAAAAAABF-M/QL1q6Cgld6Y/s1600/python.png) 
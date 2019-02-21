---
title: "Playing around with Python"
date: '2013-08-22T12:30:00.000+02:00'
search: true
comments: true
published: true
tags:
- python
---

So I've been looking for a creative outlet for this very busy brain of mine, and TSQL doesn't seem to fit the bill so much. I looked into Java and Python and seeing that Python is an interpreted language, I've decided to give it a go. 

And it seemed only fair that one of the first things I did with it was weightlifting related. One of the beginning chapters discussed mostly mathematical equations and all I could think of was how many plates should be on the bar. 

Here’s what I did, and I’m pretty sure there’s easier ways to this, but this is what I have and lank proud of it. 

```python
# setup
measure = 'kg' # use kg or lbsincrement = 2.5 # round to the nearestbarweight = 20.0
# enter the desired weight on the bar
weigth = eval(input('Enter the weight: '))
# rounded weight
weight = increment * round(weigth / increment)
# weight without the bar
weightwobar = weight - barweight
# weight on one side of the bar
weightoneside = weightwobar / 2
remainingWeight = weightoneside
# number of 20's
numberOf20 = int(remainingWeight // 20)remainingWeight = remainingWeight % 20
# number of 15's
numberOf15 = int(remainingWeight // 15)remainingWeight = remainingWeight % 15
# number of 10's
numberOf10 = int(remainingWeight // 10)remainingWeight = remainingWeight % 10
# number of 5's
numberOf5 = int(remainingWeight // 5)remainingWeight = remainingWeight % 5
# number of 2.5's
numberOf2and5 = int(remainingWeight // 2.5)remainingWeight = remainingWeight % 2.5
# number of 1.25's
numberOf1and25 = int(remainingWeight // 1.25)remainingWeight = remainingWeight % 1.25
# Display the results
print('Your weight', weigth, measure, '( rounded to the closest', increment, measure, '=', weight, measure,') consists ofn','n'
't', numberOf20, 'x 20kg plates', ' =', numberOf20 * 20, measure,'n','t', numberOf15, 'x 15kg plates', ' =', numberOf15 * 15, measure,'n','t', numberOf10, 'x 10kg plates', ' =', numberOf10 * 10, measure,'n','t', numberOf5, 'x 5kg plates', ' =', numberOf5 * 5, measure,'n','t', numberOf2and5, 'x 2.5kg plates', ' =', numberOf2and5 * 2.5, measure,'n','t', numberOf1and25, 'x 1.25kg plates', ' =', numberOf1and25 * 1.25, measure,'n','t', ' ', (numberOf20 * 20)+(numberOf15 * 15)+(numberOf10 * 10)+(numberOf5 * 5)+(numberOf2and5 * 2.5)+(numberOf1and25 * 1.25), measure, 'n',
) 
```

This prompts one for the amount of weight and will then output the individual 
plates required. 

![results](/images/playing-around-with-python-001.png)

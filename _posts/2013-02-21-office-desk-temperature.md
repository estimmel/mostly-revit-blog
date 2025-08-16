---
layout: post
title: Office Desk Temperature  
date: 2013-02-21 23:04:00 
author: Eric Stimmel  
tags: [arduino, data, temperature, humidity, cosm]
abstract: Here's a simple graph of the temperature at my desk at work.  
---

Here's a simple graph of the temperature at my desk at work over the last 24 hours. It's using a [temperature and humidity][1] sensor hooked up to an old [Arduino NG][2] and sending data to a custom console application that uploads to [Cosm.com][3].

```
<img src=https://api.cosm.com/v2/feeds/92748/datastreams/Temperature.png?width=748&height=250&colour=%23f15a24&duration=1day&legend=Temperature%20(%C2%B0C)&title=Temperature%20at%20My%20Desk&stroke_size=6&show_axis_labels=true&detailed_grid=true&scale=auto&timezone=UTC>
```

The sensor I'm using also measure humidity, so I've been logging that as well. Here is a graph of the same time period showing the humidity.

```
<img src=https://api.cosm.com/v2/feeds/92748/datastreams/Humidity.png?width=748&height=250&colour=%23f15a24&duration=1day&legend=Humidity%20(%25)&title=Humidity%20at%20My%20Desk&stroke_size=6&show_axis_labels=true&detailed_grid=true&scale=auto&timezone=UTC>
```

You might ask 'What does this have to do with Revit?' or 'Why are you doing this?' The answer is partly that I have a great interest in data, data visualization and the [IoT][4]. I also believe that part of the value in moving to systems, like Revit, that makes embedded data practically inevitable if not friendlier and more accessible, is that we can start to do some real, testable research. We can do simulations in software and then we can compare that to real data like what I've shown above.

It's far from reliable at this point, but it's a start.

**UPDATE**: Obviously the links above don't work anymore and at this point, I'm not sure if I ever captured an image to replace the live link, but if I find one, I'll add it in. For now, I just preserved the api call in a code block. ¯\\\_(ツ)\_/¯

[1]: https://www.sparkfun.com/products/8257  
[2]: http://arduino.cc/en/main/boards  
[3]: https://cosm.com/feeds/92748  
[4]: http://en.wikipedia.org/wiki/Internet_of_Things
---
layout: post
title: Detail Groups vs. Detail Components  
date: 2012-07-17 16:11:00  
author: Eric Stimmel  
tags: [revit, drafting]  
abstract: A simple evaluation of file size when using detail components vs. detail groups. Spoiler - detail components are more efficient.
---

I'm sure this has been done before, but here's a simple file size comparison for using detail **components** vs. using detail **groups**. I took a simple 1x4 and made a detail group out of this using six lines and arrayed it 100 times in one direction and arrayed the array 100 times in the other direction. You can see images of it below. I then took the out-of-the-box Revit detail component of a 1x4 and inserted that into a new file starting from the same template and arrayed it the same way. I then saved the files as new files (to compress them) and checked the file sizes. I did the same thing for one instance for both the detail component and the detail group.

The results are telling - the single instance files are exactly the same size, but the file with 10,000 instances of the detail group is more than twice the size of the corresponding file using detail components. Now, I admit, 10,000 instances is a lot of instances so I did the math[^fn-math] and using the detail group ended up adding about 100 bytes per line. That could add up to something not too insignificant.

![one instance][]  
![10000 instances][]  
![file sizes][]

  [^fn-math]: (9,808 KB - 4,044 KB) / 10,000 instances = 0.58 KB If you round that up to 0.60 or 600 bytes per detail group and considering that each detail group contains six lines, that's roughtly 100 bytes per line. I should really have more sample data to be making this claim...  
  
  [one instance]: http://ericstimmel.com/blog_imgs/1-instance.png  
  [10000 instances]: http://ericstimmel.com/blog_imgs/10000-instances.png  
  [file sizes]: http://ericstimmel.com/blog_imgs/group-vs-component-file-size.png  
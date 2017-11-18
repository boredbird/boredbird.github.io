---
title: Error Analysis (Post-Modeling)
date: 2017-10-07 14:44:02 
categories: "机器学习" 
tags: 
     - 特征工程
description: Error Analysis (Post-Modeling)
---

**Error analysis** is a broad term that refers to analyzing the misclassified or high error observations from your model and deciding on your next steps for improvement. This is performed after training your first model.

Possible next steps include collecting more data, splitting the problem apart, or engineering new features that address the errors. To use error analysis for feature engineering, you'll need to understand why your model missed its mark.

Here's how:

* **Start with larger errors:** Error analysis is typically a manual process. You won't have time to scrutinize every observation. We recommend starting with those that had higher error scores. Look for patterns that you can formalize into new features.
* **Segment by classes:** Another technique is to segment your observations and compare the average error within each segment. You can try creating indicator variables for the segments with the highest errors.
* **Unsupervised clustering:** If you have trouble spotting patterns, you can run an unsupervised clustering algorithm on the misclassified observations. We don't recommend blindly using those clusters as a new feature, but they can make it easier to spot patterns. Remember, the goal is to understand why observations were misclassified.
* **Ask colleagues or domain experts:** This is a great complement to any of the other three techniques. Asking a domain expert is especially useful if you've identified a pattern of poor performance (e.g. through segmentations) but don't yet understand why.
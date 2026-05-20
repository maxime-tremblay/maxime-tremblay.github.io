---
layout: post
title: Using AutoNumeric.js in your Applications
tags: [JavaScript, Forms]
---

Have you ever been asked to have number based items (eg. amount items, percentages, numbers, etc.) of your applications accept numbers only?

I certainly did. Funny thing is that I was asked the same thing more than once in the last couple of weeks by multiple people.
I thought it would be great to share with everyone how I do it.

Over time, I used different solutions always trying to improve upon previous versions.
Back then, the initial requirement was very simple. So everything was done using simple custom JavaScript code.
After some time and some change requests, that custom code grew in size and complexity so that it was able to handle additionnal features (e.g. copy/paste, backspace, delete, automatic formating, etc.

At that point, I decided it would be better to start using a third party library.

After some searching and testing, I decided to use the [AutoNumeric](http://autonumeric.org/){:target="_blank"} JavaScript library.
>autoNumeric is a standalone Javascript library that provides live as-you-type formatting for international numbers and currencies.

Let's get started.

## 1. Integration
First thing you'll need to do include the library in your application. For this you can use one of the following option:
 - Use the [CDN link](https://www.npmjs.com/package/autonumeric){:target="_blank"} directly in your application
 - Download the JS file from CDN and import it in your application
 - Get the [NPM pacakge](https://www.npmjs.com/package/autonumeric){:target="_blank"} and import the JS files in your application

## 2. Configuration


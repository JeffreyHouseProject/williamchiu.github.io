---
layout: post
title: Beep Boop
---

## Automated Redditing
There are lots of reddit bots made using Python. On the other hand, very few are made using Java. This is for good reason...

But I'm stubborn and don't have a good grasp of Python so Im gonna use Processing.

### JReddit
While Python has PRAW, the Python Reddit API Wrapper, Java has JReddit... Java-Reddit? Thats the wrapper that I used. It also is a wrapper that does not use OAuth2, so I'll have to make the jump to JRAW in the future.

First, you need to download the wrapper. I downloaded all the dependencies manually from the Maven site. There also were a few unlisted dependencies on the JReddit Github page.

Drag these dependencies into your sketch. With my limitted understanding of how they work, I just think of them as external classes.

So, you should have a folder with your sketch namme. I named mine "sadistbot".

Inside this folder is the .pde as well as a folder called code with your downloaded .jar files.

With this, move on to write your bot.

### Beep Boop
Processing is very good with introducing people to programming. It has methods that are easy to understand. void setup() runs once... void draw() runs continuously etc. We'll use this to our advantage when writing the bot.

First, at the top of your sketch, copy paste this.

```java
import java.io.BufferedReader;
import java.io.FileNotFoundException;
import java.io.FileReader;
import java.io.IOException;
import java.util.*;
```

With your dependencies installed and the above imported, you could proceed to refer to the "implemented methods" page on the JReddit github. Then, you could write your bot.

[Check out sadistbot on github](www.google.com)






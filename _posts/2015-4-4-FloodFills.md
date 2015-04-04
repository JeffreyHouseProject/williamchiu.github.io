---
layout: post
title: The "Paintbucket"
---

## The thing with flood fills.
In image editing software, you see paintbuckets all the time. 

In photoshop, for example, the paintbucket is the tool that fills in an area that share the same color.

Could the same thing be done on Processing?

### What are flood fills?
When you fill an area of a photo using a paintbucket tool, what are you doing?

According to [Google](https://www.google.com/search?q=program+paintbucket&oq=program+paintbucket&aqs=chrome..69i57.2758j0j1&sourceid=chrome&es_sm=91&ie=UTF-8#q=how+do+fill+tools+work), you are using a floodfill.

According to Wikipedia
>Flood fill, also called seed fill, is an algorithm that determines the area connected to a given node in a multi-dimensional array. It is used in the "bucket" fill tool of paint programs to fill connected, similarly-colored areas with a different color..

Essentially, flood fill is an algorithm for finding connected space. In the case of a paintbucket tool, the "connected space" would be areas of uniform color.

### Finding Pseudo Code
Wikipedia also has some pretty helpful pseudo code. Look at this example:

```
Flood-fill (node, target-color, replacement-color):
 1. If target-color is equal to replacement-color, return.
 2. If the color of node is not equal to target-color, return.
 3. Set the color of node to replacement-color.
 4. Perform Flood-fill (one step to the west of node, target-color, replacement-color).
    Perform Flood-fill (one step to the east of node, target-color, replacement-color).
    Perform Flood-fill (one step to the north of node, target-color, replacement-color).
    Perform Flood-fill (one step to the south of node, target-color, replacement-color).
 5. Return.
 ```


---
layout: post
title: The "Paintbucket"
---

## Flood fills are stupid
Its easy to take the paintbucket tool for granted when it appears in every image editor out there.

In photoshop, for example, the paintbucket is the tool that fills in an area that share the same color.

.. But how do we do the same thing on Processing?

### What are flood fills?
When you fill an area of a photo using a paintbucket tool, what are you doing?

According to [Google](https://www.google.com/search?q=program+paintbucket&oq=program+paintbucket&aqs=chrome..69i57.2758j0j1&sourceid=chrome&es_sm=91&ie=UTF-8#q=how+do+fill+tools+work), you are using a floodfill.

A floodfill?

A flood fill is an algorithm for finding connected space. In the case of a paintbucket tool, the "connected space" would be areas of uniform color.

Cool. Now to apply this to a paintbucket tool.

### Finding Pseudo Code
Wikipedia has some pretty helpful pseudo code in the floodfill page. Look at this example:

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
 
This method takes a node (to indicate a spot), a target-color, and a replacement-color. It performs checks on the node and replaces its color if the node is of the target-color. Then it calls itself again for all the spots around the node so as to cover the entire area. By doing this, the method successfully fills an entire area with the replacement-color.
 
Cool. Lets try this in Processing.
 
### Processing Attempt No 1
From that heading, you probably already have an idea of how this is gonna go.
 
Anyways, here was Processing code that I thought reflected the Flood-fill pseudo code.

```java
void setup() {
size(700, 1200);
rect(0, 0, 50, 50);
}

void draw(){
}

void mousePressed() {
  floodFill(mouseY * width + mouseX, get(mouseX, mouseY), color(255, 0, 0));
}

void floodFill(int pixelNumber, color targetColor, color replacementColor) {
  loadPixels();
  if (targetColor != replacementColor) {
    if (pixels[pixelNumber] == targetColor) {
      pixels[pixelNumber] = replacementColor;
      updatePixels();
      floodFill(pixelNumber + 1, targetColor, replacementColor);
      floodFill(pixelNumber - 1, targetColor, replacementColor);
      floodFill(pixelNumber + width, targetColor, replacementColor);
      floodFill(pixelNumber - width, targetColor, replacementColor);
    }
  }
}
```

Don't waste your time testing this junk. Its slow and only works when you click a small area.

When you click outside of the 50 x 50 square, you get an error something like this..

```
crashed in event thread due to Timeout occurred while waiting for packet 4296.
org.eclipse.jdi.TimeoutException: Timeout occurred while waiting for packet 4296.
	at org.eclipse.jdi.internal.connect.PacketReceiveManager.getReply(PacketReceiveManager.java:186)
	at org.eclipse.jdi.internal.connect.PacketReceiveManager.getReply(PacketReceiveManager.java:197)
	at org.eclipse.jdi.internal.MirrorImpl.requestVM(MirrorImpl.java:191)
	at org.eclipse.jdi.internal.MirrorImpl.requestVM(MirrorImpl.java:226)
	at org.eclipse.jdi.internal.ThreadReferenceImpl.frames(ThreadReferenceImpl.java:257)
	at org.eclipse.jdi.internal.ThreadReferenceImpl.frames(ThreadReferenceImpl.java:240)
	at processing.mode.java.runner.Runner.findException(Runner.java:888)
	at processing.mode.java.runner.Runner.reportException(Runner.java:871)
	at processing.mode.java.runner.Runner.exceptionEvent(Runner.java:797)
	at processing.mode.java.runner.Runner$2.run(Runner.java:688)
```

What is this? I have no clue. When I did this the first time I got a stack overflow. However, I'm pretty sure that both could be solved by getting rid of the recursive calls.

Lets look at another Wikipedia pseudo code.

```
Flood-fill (node, target-color, replacement-color):
 1. If target-color is equal to replacement-color, return.
 2. Set Q to the empty queue.
 3. Add node to the end of Q.
 4. While Q is not empty: 
 5.     Set n equal to the first element of Q.
 6.     Remove first element from Q.
 7.     If the color of n is equal to target-color:
 8.         Set the color of n to replacement-color and mark "n" as processed.
 9.         Add west node to end of Q if west has not been processed yet.
 10.        Add east node to end of Q if east has not been processed yet.
 11.        Add north node to end of Q if north has not been processed yet.
 12.        Add south node to end of Q if south has not been processed yet.
 13. Return.
```

To implement an equivalent in Processing, we could use an Arraylist and a while loop.

### Processing Attempt No 2
```java
import java.util.ArrayList;

void setup() {
  size(700, 1200);
  rect(0, 0, 500, 500);
}

void draw() {
}

void mousePressed() {
  floodFill(mouseY * width + mouseX, get(mouseX, mouseY), color(255, 0, 0));
}

void floodFill(int pixelNumber, color targetColor, color replacementColor) {
  ArrayList<Integer> queue = new ArrayList<Integer>();
  loadPixels();
  queue.add(pixelNumber);
  while (!queue.isEmpty()) {
    if (targetColor != replacementColor && queue.get(0) < width * height && queue.get(0) > 0) {
      if (pixels[queue.get(0)] == targetColor) {
        pixels[queue.get(0)] = replacementColor;
        queue.add(queue.get(0) + 1);
        queue.add(queue.get(0) - 1);
        queue.add(queue.get(0) + width);
        queue.add(queue.get(0) - width);
      }
    }
    queue.remove(0);
  }
  updatePixels();
}
```

And thats it!




 


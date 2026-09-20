---
Priority_Level: 4 Low
Status: 4 Completed
Date_Created: 
Due_Date: 
connections: 
tags:
  - "#project/mandelbrot"
type: project_note
cssclasses:
  - hide-properties_editing
  - hide-properties_reading
closed: 2025-02-22T15:33
_previous_status: 1 To Do
---
# Components
**Select Connection:** `INPUT[inlineListSuggester(optionQuery(#area)):connections]` 
**Date Created:** `INPUT[dateTime(defaultValue(null)):Date_Created]`
**Due Date:** `INPUT[dateTime(defaultValue(null)):Due_Date]`
**Priority Level:** `INPUT[inlineSelect(option(1 Critical), option(2 High), option(3 Medium), option(4 Low)):Priority_Level]`
**Status:** `INPUT[inlineSelect(option(1 To Do), option(2 In Progress), option(3 Testing), option(4 Completed), option(5 Blocked)):Status]`
# Description


> This project was inspired by an excellent list of challenging projects shared [here](https://www.andreinc.net/2024/03/28/programming-projects-ideas#write-a-tiling-window-manager). It's an ideal opportunity to sharpen my Rust programming skills while also diving into WebAssembly. 

Mandelbrot set is one of the fascinating objects in mathematics, as it has an easy definition but the result is extremely complex. Its beautiful nature not only inspired mathematicians, but also artists, like David Hockney for a painting and John Updike in some pages.

Zooming in you can find copies of itself, seahorse structures, spirals, islands and many other interesting structures. It illustrates how profound intricacy can emerge from the simplest of rules — much like life itself[^1]. 

The formal definition states that it is the set obtained from the quadratic recurrence equation
$$
z_{n+1} = z_n + c
$$
with $z_0= c$, where points $c$ for which the orbit of $z_n$ does not tend to infinity are in the set [^2] . This means that a complex number $c$ belongs to the set if, when starting from $z_0=0$ and applying the iteration, $|z_n|$ remains bounded $\forall n>0$.

Since I am not a mathematician, I don't want to spend too much time on the mathematical details right now and I'll skip directly to the plotting algorithms, starting from the simplest one, the **Escape time algorithm**.

# Escape Time algorithm
This algorithm determines how quickly the sequence escapes to infinity for each point of the complex plane. It assigns a color to each pixel based on the number of iterations it takes for the magnitude of $z_n$ to reach a certain threshold. The algorithm can be written like this:
```pseudo
    \begin{algorithm}
    \caption{Escape Time algorithm}
    \begin{algorithmic}
	    \For{each pixel $(P_x,P_y)$}
	    \State $x_0 \leftarrow $ scaled x coordinate of $P_x$
	    \State $y_0 \leftarrow $ scaled y coordinate of $P_y$
	    \State iteration $\leftarrow $ 0
		\While{$x^2 + y^2 < 4$ and iteration < max\_iteration}
		\State $x\_{temp} \leftarrow x^2 - y^2 + x_0$
		\State $y\leftarrow 2xy + y_0$
		\State $x\leftarrow x_{temp}$
		\State iteration $\leftarrow$ iteration + 1
        \EndWhile
        \State color $\leftarrow$ palette[iteration]
        \EndFor  
    \end{algorithmic}
    \end{algorithm}
```
The values are checked during each iteration to see whether they have reached a critical "escape" condition, or "bailout". If that condition is reached, the calculation is stopped, the pixel is drawn, and the next _x_, _y_ point is examined. For values within the Mandelbrot set, escape will never occur, so a bail condition (in the pseudo code $max\_iteration$) should be set.

With this simple algorithm, this is the result:
![[mandelbort_v1.png]]
As can be seen in the Figure above, these simple method creates some bands of color, which are not attractive as the smooth colors. The problem is that the number of iterations until escape is an integer, resulting in a stair-step function. It is sufficient to transform the iteration count like this:
$$
m = n + 1 - \frac{ \ln\ln|z|}{\ln2}
$$
where $n$ is the iteration count found by the naive escape algorithm and $|z|$ its the norm of the complex number at exit.
The result is the following:
![[mandelbrot_v1_5.png]]
much better!


[^1]: https://www.quantamagazine.org/the-quest-to-decode-the-mandelbrot-set-maths-famed-fractal-20240126/
[^2]: https://mathworld.wolfram.com/MandelbrotSet.html


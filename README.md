# Polygons
Drawing a polygon is an easy task, just find the angles and use your protractor and compass to draw the polygon, however not everyone has those tools readily available.
Thankfully using complex numbers we can find an elegent and simple solution to finding the x,y coordinates of any polygon

## The roots of unity

Lets say we have the equation $z^3 = 1$, an obvious solution for this is z = 1, but an n degree polynomial should have n solutions. So to get the other 2 solutions we factor out $(z-1)$ from $(z^3-1)$ we get $(z-1)(z^2+z+1) = 0$

Solving $z^2 +z +1 = 0$ we get $z = -\frac{1}{2} \pm \frac{\sqrt{3}}{2}i$, these 3 solutions are the *cube roots of unity*. If we draw these points on an Argand diagram we get the 3 points at $60\degree$ angles of one another, each of length 1.
<div>
<img src="image.png" width="500"/>
</div>

Joining these points together we get a 3 sided polygon 
<div>
<img src="image2.png" width="500"/>
</div>

This is the general procedure we will use to find the coordinates of any polygon. For an **n** sided polygon, find the solutions of the **nth** root of unity. Now we need to generalize the proceess of finding these solutions as easily as possible

## Finding the **nth** root of unity

An equation $z^n = 1$ has n solutions and using 1 in polar form is $1 = \cos(0 + 2\pi k) + i \sin(0 + 2\pi k)$

Now using de Moivre's theorem, we can see than $z = \cos \left(\frac{2\pi k}{n} \right) + i \sin \left(\frac{2\pi k}{n} \right), k = \{1,2,...,n\}$

Using this formula we can easily find the coordinates of any polygon

```py
from math import sin, cos, pi

# returns a list of (x,y) coordinates
def polygon(n : int):
    coordinates = []
    for k in range(n):
        x = cos(2*pi*k/n)
        y = sin(2*pi*k/n)

        coordinates.append((x,y))

    return coordinates
```

We can also add a rotation to this formula. Lets say we wish to rotate by T degrees, first we have to convert to T radians.
Now $z = \cos \left(\frac{T + 2\pi k}{n} \right) + i \sin \left(\frac{T + 2\pi k}{n} \right), k = \{1,2,...,n\}$

```py
# returns a list of (x,y) coordinates for n sided polygon at T degrees
def polygon(n : int, T : float = 0):
    #convert to radians
    T *= pi/180

    coordinates = []
    for k in range(n):
        x = cos((T + 2*pi*k)/n)
        y = sin((T + 2*pi*k)/n)

        coordinates.append((x,y))
  return coordinates
```
    

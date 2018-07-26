[![Build Status](https://travis-ci.org/ryu577/pyray.svg?branch=master)](https://travis-ci.org/ryu577/pyray)

Pyray 是一个基于Python 的3D 渲染库。现在，POV ray 是一个很棒的程序，但我们为什么不能在Python 中开发一个同样功能的应用程序，用于2D，3D 和更高维度的对象和场景渲染呢？在这个项目中我将用Python 展示POV ray 程序所能做的一切，包括渲染复杂的3D 对象、场景、动画等

# Introduction

I'm creating this repository in January 2018 and it is crazy that the best open source option for rendering 3d scenes remains POV ray.
Now, POV ray is a great program, but why can't we have that functionality (rendering 2d, 3d and higher dimensional objects and scenes) in Python, a language that is perhaps the most widely used already and only growing in popularity?
This code is a first step towards that goal - have the ability to do everything POV ray does - rendering complex 3d objects and scenes, animations and much more in plain, vanilla Python. I imagine this would find applications in creating videos, video games, physical simulations or just pretty pictures.

While there certainly is a very long way to go before this can be a reality, it won't happen without taking a first step. And of course, I could use help :)

Above all else, I want to emphasize simplicity in this library and minimize the dependence on external libraries so more people can hit the ground running with it.


# Installation
To install the library, run (pyray was taken on pypi):

```
pip install raypy
```

Make sure you have all the requirements (requirements.txt) installed. If not, you can run:

```
pip install -r requirements.txt
```

Alternately, you can fork/download the code and run from the main folder:

```
python setup.py install
```

# Demonstrations
So far, I've been using this to create YouTube videos for <a href="https://www.youtube.com/channel/UCd2Boc12Ora42VIJBULz0kA">my channel</a>.

Here are some that demonstrate the abilities of this code (also see below for some images created with it) - 

1. <a href="https://www.youtube.com/watch?v=KuXnrg1YpiY">Binomial coefficients on hypercubes.</a>

2. <a href="https://www.youtube.com/watch?v=OV7c6S32IDU&t=3s">Why does Gradient descent work?</a>

3. <a href="https://www.youtube.com/watch?v=STkcP5jcJYo">Introduction to Platonic solids</a>

4. <a href="https://www.youtube.com/watch?v=57g6nQGBFcY">Slice a 4d hypercube (Teserract).</a>

# Requirements
I've made every effort to keep the requirements for this project to the bare minimum so most people can get it running with almost no pain. These are - 
Python Imaging Library (PIL), numpy and scipy. For writing on math equations images using the methods in WriteOnImage.py, you'll need matplotlib and sympy. All of these can be installed quite easily with `pip install -r requirements.txt`

# Usage
To keep things simple and the dependencies minimal, the program simply writes an image or a series of images to the folder `./Images/RotatingCube` (this was the first object that was animated with this tool). 

You can run any method tagged @MoneyShot to see how this works. For example, you can run the following method from cube.py - 

```python
from pyray.shapes.cube import *
cube_with_cuttingplanes(7, popup=True)
```
and this will generate a colorful 3d cube with diagonal cutting planes shaded in different colors (in the folder where you run it from, file called im0.png). Something like this - 

<a href="http://www.youtube.com/watch?feature=player_embedded&v=KuXnrg1YpiY" 
target="_blank"><img src="https://github.com/ryu577/pyray/blob/master/Images/cube_planes.png" 
alt="Image formed by above method" width="240" height="240" border="10" align="center"/></a>


You can now create a series of them using the following code - 

```python
for i in range(3, 15):
	cube_with_cuttingplanes(numTerms = i, im_ind = i-3)
```

The series of images can then be easily converted to a video using the open source <a href="https://ffmpeg.org/download.html">ffmpeg program</a>. For example

> ffmpeg -framerate 10 -f image2 -i im%d.png -vb 20M vid.avi

The video can then be converted to a .gif file if required - 

> ffmpeg -i vid.avi -pix_fmt rgb24 -loop 0 out.gif

For example, something like this:


<a href="https://www.youtube.com/watch?v=OV7c6S32IDU" 
target="_blank"><img src="https://github.com/ryu577/ryu577.github.io/blob/master/Downloads/GradientAscent/which_direction.gif" 
alt="Image formed by above method" width="240" height="180" border="10" /></a>

In case you're wondering, you can generate the images used in the gif above via:

```python
from pyray.shapes.plane import *
for i in range(20):
	best_plane_direction(im_ind=i)
```


# Contributing

We welcome any kind of contribution, bug report, suggestion, new module, etc. Anything is welcome.

# Other examples

To create a bouncy sphere or a wavy sphere, run 
```python
from pyray.shapes.sphere import *
draw_wavy_sphere_wrapper('.\\im', 66, 1)
```

<img src="https://github.com/ryu577/pyray/blob/master/Images/WavySphere.gif" 
alt="Image formed by above method" width="240" height="240" border="10" /></a>

```python
draw_oscillating_sphere('..\\images\\im', 20, 2)
```
<img src="https://github.com/ryu577/pyray/blob/master/Images/BouncySphere.gif" 
alt="Image formed by above method" width="240" height="240" border="10" /></a>

```python
from pyray.shapes.polyhedron import *
basedir = '.\\'
tr = Tetartoid()
for i in range(0, 31):
    im = Image.new("RGB", (2048, 2048), (1,1,1))
    draw = ImageDraw.Draw(im,'RGBA')
    r = general_rotation(np.array([0,1,0]),2*np.pi*i/30)
    tr.render_solid_planes(draw, r, shift=np.array([1000, 1000, 0]), scale=750)
    im.save(basedir + "im" + str(i) + ".png")
```

<a href="https://www.youtube.com/watch?v=OV7c6S32IDU" 
target="_blank"><img src="https://github.com/ryu577/ryu577.github.io/blob/master/Downloads/tetartoid2.gif" 
alt="Image formed by above method" width="240" height="240" border="10" /></a>


```python
from pyray.shapes.paraboloid import *
draw_paraboloids()
```

<a href="https://www.youtube.com/watch?v=OV7c6S32IDU" 
target="_blank"><img src="https://github.com/ryu577/ryu577.github.io/blob/master/Downloads/paraboloids.gif" 
alt="Image formed by above method" width="240" height="240" border="10" /></a>



```python
from pyray.shapes.pointswarm import *
points_to_bins()
```

<a href="https://www.youtube.com/watch?v=OV7c6S32IDU" 
target="_blank"><img src="https://github.com/ryu577/ryu577.github.io/blob/master/Downloads/classificn/classificn.gif" 
alt="Image formed by above method" width="240" height="240" border="10" /></a>


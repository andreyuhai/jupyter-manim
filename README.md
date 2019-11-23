# jupyter-manim
[![MIT License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat)](http://choosealicense.com/licenses/mit/)


Integrates [manim](https://github.com/3b1b/manim) (animation engine for explanatory math videos)
with Jupyter displaying the resulting video when using `%%manim` cell magic to wrap a scene definition.

### Quick preview

<img src='screenshots/cell_magic_demo.png'>

The code in the example above comes from the excellent [manim tutorial](https://github.com/malhotra5/Manim-Tutorial).

### Installation

```sh
pip3 install jupyter-manim
```

### Usage

To enable the manim magic please run `import jupyter_manim` first. Then, you can use the magic as if it was the manim command: your arguments will be passed to manim, exactly as if these were command line options.

For example, to render scene defined with class `Shapes(Scene)` use

```python
%%manim Shapes
from manimlib.scene.scene import Scene
from manimlib.mobject.geometry import Circle
from manimlib.animation.creation import ShowCreation

class Shapes(Scene):

    def construct(self):
        circle = Circle()
        self.play(ShowCreation(circle))
```

NOTE: currently the code has to be self-contained as it will be run in a separate namespace.
Thus, all the imports have to be contained in your cell.

In future, an option to export the current namespace (or specific variables) will be added.
It could be implemented by pickling the Python locals and globals and then pre-pending the cell with an un-pickling script (PRs welcome!).

In the latest version of manimlib you can import everything at once using:

```python
from manimlib.imports import *
```


To display manim help and options use:

```
%%manim -h
pass
```



The `%%manim` magic (by default) hides the progress bars as well as other logging messages generated by manim.
You can disable this behaviour using `--verbose` flag

#### Video player control options

 - `--no-controls` - hides the controls
 - `--no-autoplay` - disables the autoplay feature
 - `-r` or `--resolution` - control the height and width of the video player;
  this option is shared with manim and requires the resolution in following format:
  `height,width`, e.g. `%%manim Shapes -r 200,1000`
 - `--remote` send the video with a `data:` URL instead of a local path (useful for remote notebooks like Google Colab)

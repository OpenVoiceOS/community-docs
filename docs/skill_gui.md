## GUI framework

Mycroft-GUI is an open source visual and display framework for Mycroft running on top of KDE Plasma Technology and built using Kirigami a lightweight user interface framework for convergent applications which are empowered by Qt.

OVOS uses the standard mycroft-gui framework, you can find the official documentation [here](https://mycroft-ai.gitbook.io/docs/skill-development/displaying-information/mycroft-gui)

OVOS images are powered by [ovos-shell](https://openvoiceos.github.io/community-docs/shell/), the client side implementation of the gui protocol

## Show Simple Content

### Text

Display simple strings of text.

```python
self.gui.show_text(self, text, title=None, override_idle=None, override_animations=False)
```

Arguments:

* text \(str\): Main text content.  It will auto-paginate
* title \(str\): A title to display above the text content.
* override\_idle \(boolean, int\):
  * True: Takes over the resting page indefinitely
  * \(int\): Delays resting page for the specified number of seconds.
* override\_animations \(boolean\):
  * True: Disables showing all platform skill animations.
  * False: 'Default' always show animations.

### Static Image

Display a static image such as a jpeg or png.

```python
self.gui.show_image(self, url, caption=None, title=None, fill=None, override_idle=None, override_animations=False)
```

Arguments:

* url \(str\): Pointer to the image
* caption \(str\): A caption to show under the image
* title \(str\): A title to display above the image content
* fill \(str\): Fill type - supports: 
  * 'PreserveAspectFit',
  * 'PreserveAspectCrop', 
  * 'Stretch'
* override\_idle \(boolean, int\):
  * True: Takes over the resting page indefinitely
  * \(int\): Delays resting page for the specified number of seconds.
* override\_animations \(boolean\):
  * True: Disables showing all platform skill animations.
  * False: 'Default' always show animations.

### Animated Image

Display an animated image such as a gif.

```python
self.gui.show_animated_image(self, url, caption=None, title=None, fill=None, override_idle=None, override_animations=False)
```

Arguments:

* url \(str\): Pointer to the .gif image
* caption \(str\): A caption to show under the image
* title \(str\): A title to display above the image content
* fill \(str\): Fill type - supports: 
  * 'PreserveAspectFit',
  * 'PreserveAspectCrop', 
  * 'Stretch'
* override\_idle \(boolean, int\):
  * True: Takes over the resting page indefinitely
  * \(int\): Delays resting page for the specified number of seconds.
* override\_animations \(boolean\):
  * True: Disables showing all platform skill animations.
  * False: 'Default' always show animations.

### HTML Page

Display a local HTML page.

```python
self.gui.show_html(self, html, resource_url=None, override_idle=None, override_animations=False)
```

Arguments:

* html \(str\): HTML text to display
* resource\_url \(str\): Pointer to HTML resources
* override\_idle \(boolean, int\):
  * True: Takes over the resting page indefinitely
  * \(int\): Delays resting page for the specified number of seconds.
* override\_animations \(boolean\):
  * True: Disables showing all platform skill animations.
  * False: 'Default' always show animations.

### Remote URL

Display a webpage.

```python
self.gui.show_url(self, url, override_idle=None, override_animations=False)
```

Arguments:

* url \(str\): URL to render
* override\_idle \(boolean, int\):
  * True: Takes over the resting page indefinitely
  * \(int\): Delays resting page for the specified number of seconds.
* override\_animations \(boolean\):
  * True: Disables showing all platform skill animations.
  * False: 'Default' always show animations.


## GUI Framework

Mycroft-GUI is an open source visual and display framework for Mycroft running on top of KDE Plasma Technology and built using Kirigami a lightweight user interface framework for convergent applications which are empowered by Qt.

OVOS uses the standard mycroft-gui framework, you can find the official documentation [here](https://mycroft-ai.gitbook.io/docs/skill-development/displaying-information/mycroft-gui)

OVOS images are powered by [ovos-shell](https://openvoiceos.github.io/community-docs/shell/), the client side implementation of the gui protocol

## GUI Extensions
OVOS Core supports a GUI Extension framework which allows the GUI service to incorporate additional behaviour for a specific platform. GUI Extensions currently supported:

##### Smartspeaker Extension: 
This extension is responsible for managing the smartspeaker GUI interface behaviour, it supports homescreens and homescreen management. Enabling the smartspeaker GUI extension: 
```
  "gui": {
    "extension": "smartspeaker",
    "idle_display_skill": "skill-ovos-homescreen.openvoiceos"
  }
```

##### Bigscreen Extension: 
This extension is responsible for managing the plasma bigscreen GUI interface behaviour, it supports window management and window behaviour control on specific window managers like Kwin. Enabling the Bigscreen GUI extension:
```
  "gui": {
    "extension": "bigscreen"
  }
```

##### Mobile Extension:  
This extension is responsible for managing the mobile GUI interface behaviour, it supports homescreens and additionally adds support for global page back navigation. Enabling the Mobile GUI extension:
```
  "gui": {
    "extension": "smartspeaker",
    "idle_display_skill": "skill-android-homescreen.openvoiceos"
  }
```

##### Generic Extension: 
This extension provides generic behaviour for the GUI interface and does not add any additional bheaviour, it optionally supports homescreens and which is required by the platform or user to manually enable it, if required. This extension is enabled by default when no other extension is specified.

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

## Advanced QML Code and Design Guidelines
Mycroft-GUI frameworks provides you with some base delegates you should use when desiging your QML GUI. The base delegates provide you with a basic presentation layer for your skill with some property assignments that can help you setup background images, background dim to give you the control you need for rendereing an experience. 

Before we dive deeper into the Design Guidelines, lets look at some concepts that a GUI developer should learn about:

### Units & Themeing
##### Units: 
Mycroft.Units.GridUnit is the fundamental unit of space that should be used for all sizing inside the QML UI, expressed in pixels. Each GridUnit is predefined as 16 pixels
```
// Usage in QML Components example
width: Mycroft.Units.gridUnit * 2 // 32px Wide
height: Mycroft.Units.gridUnit // 16px Tall
```
##### Themeing:
OVOS Shell uses a custom Kirigami Platform Theme plugin to provide global themeing to all our skills and user interfaces, which also allows our GUI's to be fully compatibile with the system themes on platforms that are not running the OVOS Shell.

Kirigami Theme and Color Scheme guide is extensive and can be found [here](https://develop.kde.org/docs/use/kirigami/style-colors/)

OVOS GUI's developed to follow the color scheme depend on only a subset of available colors, mainly:
1. Kirigami.Theme.backgroundColor = Primary Color (Background Color: This will always be a dark palette or light palette depending on the dark or light choosen color scheme)
2. Kirigami.Theme.highlightColor = Secondary Color (Accent Color: This will always be a standout palette that defines the themes dominating color and can be used for buttons, cards, borders, highlighted text etc)
3. Kirigami.Theme.textColor = Text Color (This will always be an opposite palette to the selected primary color)

#### QML Delegate Design Best Practise
__Let's look at this image and qml example below, this is a represntation of the Mycroft Delegate:__
![](https://mycroft.blue-systems.com/display-1.png)
1. When designing your first QML file, it is important to note the red triangles in the above image, these triangles represent the margin from the screen edge the GUI needs to be designed within, these margins ensure your GUI content does not overlap with features like edge lighting and menus in the platforms that support it like OVOS-Shell
2. The content items and components all utilize the selected color scheme, where black is the primary background color, red is our accent color and white is our contrasting text color

__Let's look at this in QML:__
```
import ...
import Mycroft 1.0 as Mycroft

Mycroft.Delegate {
    skillBackgroundSource: sessionData.exampleImage
    leftPadding: 0
    rightPadding: 0
    topPadding: 0
    bottomPadding: 0
    
    Rectangle {
        anchors.fill: parent
        // Setting margins that need to be left for the screen edges
        anchors.margins: Mycroft.Units.gridUnit * 2
        
        //Setting a background dim using our primary theme / background color on top of our skillBackgroundSource image for better readability and contrast
        color: Qt.rgba(Kirigami.Theme.backgroundColor.r, Kirigami.Theme.backgroundColor.g, Kirigami.Theme.backgroundColor.b, 0.3)
        
        Kirigami.Heading {
            level: 2
            text: "An Example Pie Chart"
            anchors.top: parent.top
            anchors.left: parent.left
            anchors.right: parent.right
            height: Mycroft.Units.gridUnit * 3
            // Setting the text color to always follow the color scheme for this item displayed on the screen
            color: Kirigami.Theme.textColor
        }
        
        PieChart {
            anchors.centerIn: parent
            pieColorMinor: Kirigami.Theme.backgroundColor // As in the image above the minor area of the pie chart uses our primary color
            pieColorMid: Kirigami.Theme.highlightColor // As in the image above the middle area is assigned the highlight or our accent color
            pieColorMajor: Kirigami.Theme.textColor // As in the image above the major area is assigned the text color
        }
    }
}
```

#### QML Delegate Multi Platform and Screen Guidelines
OVOS Skill GUI's are designed to be mutli platform and screen friendly, to support this we always try to support both Horizontal and Vertical display's. Let's look at an example and a general approach to writing multi resolution friendly UI's

__Let's look at these images below that represent a Delegate as seen in a Horizontal screen:__
![](https://mycroft.blue-systems.com/display-2.png)

__Let's look at these images below that represent a Delegate as seen in a Vertical screen:__
![](https://mycroft.blue-systems.com/display-3.png)

1. When designing for different screens it is preferred to utilize Grids, GridLayouts and GridViews this allows easier content placement as one can control the number of columns and rows displayed on the screen
2. It is also recommended to use Flickables when you believe your content is going to not fit on the screen, this allows for content to always be scrollable. To make it easier to design scrollable content, Mycroft GUI provides you with a ready to use Mycroft.ScrollableDelegate.
3. It is also preferred to use the width vs height comparision on the root delegate item to know when the screen should be using a vertical layout vs horizontal layout

__Let's look at this in QML:__
```
import ...
import Mycroft 1.0 as Mycroft

Mycroft.Delegate {
    id: root
    skillBackgroundSource: sessionData.exampleImage
    leftPadding: 0
    rightPadding: 0
    topPadding: 0
    bottomPadding: 0
    property bool horizontalMode: width >= height  ? 1 : 0 // Using a ternary operator to detect if width of the delegate is greater than the height, which provides if the delegate is in horizontalMode
    
    Rectangle {
        anchors.fill: parent
        // Setting margins that need to be left for the screen edges
        anchors.margins: Mycroft.Units.gridUnit * 2
        
        //Setting a background dim using our primary theme / background color on top of our skillBackgroundSource image for better readability and contrast
        color: Qt.rgba(Kirigami.Theme.backgroundColor.r, Kirigami.Theme.backgroundColor.g, Kirigami.Theme.backgroundColor.b, 0.3)
        
        Kirigami.Heading {
            level: 2
            text: "An Example Pie Chart"
            // Setting the text color to always follow the color scheme
            color: Kirigami.Theme.textColor
        }
        
        GridLayout {
            id: examplesGridView
            // Checking if we are in horizontal mode, we should display two columns to display the items in the image above, or if we are in vertical mode, we should display a single column only
            columns: root.horizontalMode ? 2 : 1 
            
            Repeater {
                model: examplesModel
                delegates: ExamplesDelegate {
                    ...
                }
            }
        }
    }
}
```

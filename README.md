# LiquidLoadingIndicator
Loading indicator for watchOS. Project is based on EMTLoadingIndicator but I needed some customizations, SPM compatability and implemented some fancy that would be too much to expect to get accepted for a PR.

[![License](https://img.shields.io/badge/license-MIT-blue.svg?style=flat
            )](http://mit-license.org) [![Platform](https://img.shields.io/badge/platform-watchOS-lightgrey.svg?style=flat
             )](https://developer.apple.com/resources/) [![Language](https://img.shields.io/badge/language-swift-orange.svg?style=flat
             )](https://developer.apple.com/swift) [![SPM](https://img.shields.io/badge/spm-compatible-brightgreen.svg?style=flat)](https://github.com/apple/swift-package-manager)

## Installation
Using Swift Package Manager, add `https://github.com/Reiszecke/LiquidLoadingIndicator` as a dependency, and add it to your WatchKit Extension.


## Usage

### Initialization

```swift

private var indicator: LiquidLoadingIndicator?

override func willActivate() {

    indicator = LiquidLoadingIndicator(interfaceController: self, interfaceImage: image!,
        width: 40, height: 40, style: .line)
```

width and height are the size of WKInterfaceImage passed to 2nd argument. Indicator images will be created with this size.
Style argument decides the visual of wait (loop) indicator - Dot or Line.

### Line (Circular) Indicator

This is where the project differs from the original. The original indicator could just do this:

![Image](../assets/webpage/stockline.jpeg)

```swift
indicator = LiquidLoadingIndicator(interfaceController: self, interfaceImage: image!,
    width: 40, height: 40, style: .line)
indicator?.showWait()
indicator?.hide()
```

With this repo, you can adjust parameters like line width on the object itself.

```     
indicator.setLineWidth(5.3)
indicator.setLineColor(UIColor(red: 1.0, green: 1.0, blue:1.0, alpha: 0.8))
indicator.setLineLength(0.6)
``` 

<img src="../assets/webpage/loading-indicator.gif" height="250"/>

Addionally, if you want the circular line's head and tail play catch you can look try

```
indicator.enableLavaLamp(moreBubbly: false)
```

<img src="../assets/webpage/loading-indicator-less-bubbly.gif" height="250"/>

or 

```
indicator.enableLavaLamp(moreBubbly: true)
```

<img src="../assets/webpage/loading-indicator-more-bubbly.gif" height="250"/>

It's also possible to set the viscosity (I don't know what to call this, I'm a car guy) by playing around with values such as

```
indicator.setKinetic(energy: 1.1)
```
You may not want this at all so you can do 

```
indicator.disableLavaLamp()
```

This is everything that this repo added. If you only need stuff that is mentioned below this sentence, feel free to check out the original at https://github.com/hirokimu/EMTLoadingIndicator

### Dot Indicator

![Image](../assets/webpage/stockdot.jpeg)

```swift
indicator = LiquidLoadingIndicator(interfaceController: self, interfaceImage: image!,
    width: 40, height: 40, style: .dot)

// prepareImageForWait will be called automatically in the showWait method at the first time.
// It takes a bit of time. You can call it manually if necessary.
indicator?.prepareImagesForWait()

// show
indicator?.showWait()

// hide
indicator?.hide()
```
*Images of Dot indicator are static resource files size of 80px x 80px.
 These PNG files are created with Flash CC (waitIndicatorGraphic.fla).


### Progress Indicator

![Image](../assets/webpage/stockprogress.jpeg)

```swift
indicator?.prepareImagesForProgress()

// You can set start percentage other than 0.
indicator?.showProgress(startPercentage: 0)

// Update progress percentage with animation
indicator?.updateProgress(percentage: 75)

indicator?.hide()
```

### Reload Icon

![Image](../assets/webpage/stockreload.jpeg)


You can display static reload icon (in some loading error situations).

```swift
indicator?.showReload()
```

### Styling

If you want to change styles, you need to set properties before using prepare/show methods.

```swift
// defaults
LiquidLoadingIndicator.circleLineColor = UIColor(white: 1, alpha: 0.8)
LiquidLoadingIndicator.circleLineWidth = 1
LiquidLoadingIndicator.progressLineColorOuter = UIColor(white: 1, alpha: 0.28)
LiquidLoadingIndicator.progressLineColorInner = UIColor(white: 1, alpha: 0.70)
LiquidLoadingIndicator.progressLineWidthOuter = 1
LiquidLoadingIndicator.progressLineWidthInner = 2
LiquidLoadingIndicator.reloadColor = UIColor.white
LiquidLoadingIndicator.reloadLineWidth = 4
LiquidLoadingIndicator.reloadArrowRatio = 3
```

### Clear Images

All created images are stored in static properties and used for all instances.
If you want to clear them, use following methods.

```swift
indicator?.clearWaitImage()
indicator?.clearReloadImage()
indicator?.clearProgressImage()
```

## Requirements
- watchOS 3.0+

## License
LiquidLoadingIndicator is available under the MIT license. See the LICENSE file for more info.

# MOON Graph

## Description
MOON Graph is a very simple graph library for both iOS and OS X that lets you very easily plot a graph from real-time data. We use it internally at MOON Wearables to plot real-time data from different sensors. Below you can see a screenshot and some GIFs of the graph view plotting sample data generated by compound sine waves. There's example code for both OS X and iOS in their respective folders.

![Image](http://imgur.com/P8pfcP8.png)

![Image](http://imgur.com/aBwsPs5.gif)

## API
### Overview
The entire library is just one class called `MOONGraphView`. It has a few different properties you can use to customize the appearance, and only one method. This method is called `addSample(sample: Double...)`, and this is the way you supply the graph with data. The graph currently does not automatically rescale based on the samples you've added to it. So you need to tell it the maximum and minimum values to expect.

### Properties

##### var title: String = ""
Used to set the title of the graph in one of the upper corners. The default value for this is `""`, meaning that it will not be displayed.

##### var subTitle: String = ""
Used to set a subtitle that will go right underneath the title. The default value for this is `""`, and will thus not be displayed.

##### var graphDirection = GraphDirection.RightToLeft
Specifies which way the graph will go. This is an enum with two possible options: `.LeftToRight`, and `.RightToLeft`. Setting this will also change which corner the title and subtitle will get drawn in (upper left corner for `.RightToLeft`, and vice versa). It also changes which side the values for the y-axis gets drawn (right side for `.RightToLeft`, and vice versa). The default is `.RightToLeft`.

##### var themeColor = GraphColor.Orange
This will set the background gradient of the graph. It's an enum with seven colors to pick from: `.Gray`, `.Orange`, `.Green`, `.Blue`, `.Turquoise`, `.Yellow`, and `.Purple`. The default is `.Orange`.

##### var maxSamples = 150
This sets how many samples will fit within the view. E.g., if you set this to 200, what you will see in the view is the last 200 samples. You can't set it to any lower than 2. The default value of this is 150.

##### var maxValue: CGFloat = 1.0
Determines what the maximum expected value is. It is used as an upper limit for the view. The default is 1.0.

##### var minValue: CGFloat = -1.0
Determines what the minimum expected value is. It is used as an lower limit for the view. The default is -1.0.

##### var numberOfGraphs = 1
If you want your view to draw more than one graph at the same time (say x, y, z values of an accelerometer), you can specify that using this property. Notice that the `addSamples` method takes an argument of type `Double...` (called a variadic parameter). Whatever value you set for the `numberOfGraphs` property, you need to pass in the same number of arguments to this method, otherwise it will do nothing. If you change this property, all the samples you've added so far will be removed. The default is 1, meaning the `addSamples` method takes 1 argument.

##### var roundedCorners = false
Use this to make the corners rounded or square. The default is true, meaning rounded corners.

##### var graphType = GraphType.Line
Changes how the samples are drawn. The current options are `.Line` and `.Scatter`. The default is `.Line`.

### Methods
##### func addSamples(newSamples: Double...)
This method is where you add your data to the graph. The value of the samples you add should be within the range `[minValue, maxValue]`, otherwise the graph will draw outside the view. Notice that this takes `Double...` as an argument (called a variadic parameter), which means that you can pass it one or more `Double` values as arguments. This is so that you can draw multiple graphs in the same view at the same time (say x, y, z data from an accelerometer). The number of arguments you pass needs to correspond to the `numberOfGraphs` property, otherwise this method will do nothing.

##### func reset()
Removes all the samples you've added to the graph. All the other properties like `roundedCorners` and `maxSamples` etc are kept the same. Useful if you want to reuse the same graph view.

## Todo
- Have an auto-scale feature. Might do this by having an Optional scale tuple with a min and max value. If this is nil, use auto-scale. If it's set use a fixed scale.
- Change the size of the labels when the view gets too small.
- I'm pretty sure there's a different way of doing this that will make it faster. Will probably end up drawing into a bunch of tall, skinny CALayers, and then moving them sideways.
- <del>Add IBDesignable</del>
- <del>Add scatter plot</del>

## Contact
- [@vegather on Twitter](http://www.twitter.com/vegather)

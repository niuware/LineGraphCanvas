# LineGraphCanvas

![LineGraphCanvas](http://niuware.github.io/public/assets/LineGraphCanvas/images/screen.png)

*LineGraphCanvas* is a Universal Windows Platform custom control for drawing a time progressive Line Graph (Portable to WPF as well).

## Installation

After pulling down the repository add the folders and files (Controls, Converters and Styles) to your project.

## Usage

Simply add the control to the desired Page.xaml file as follows:

```Xaml
<!-- Remember to add first the namespace -->
xmlns:controls="using:Niuware.Controls"
...

<!-- XScale is the length of the line (X axis), YScale is the scalar for the value -->
<controls:LineGraphCanvas x:Name="myLineGraphCanvas" XScale="10.0" YScale="1.0" />
```

Then in the constructor of your code Page.cs file, initialize as many values as you need to draw in the the LineGraphCanvas control:

```C#
this.InitializeComponent();
...

// If you want you can use a Label for the graph
myLineGraphCanvas.Label = "My Graph Label";

// You can graph different values in the same Line Graph
myLineGraphCanvas.AddLineGraph(0.0, "Value Label", new SolidColorBrush(Windows.UI.Colors.XXX));
...
myLineGraphCanvas.AddLineGraph(0.0, "Other N Value Label", new SolidColorBrush(Windows.UI.Colors.XXX));
```

Finally, for the drawing loop you can choose one of the following methods:

#### With CompositionTarget.Rendering 

Using the rendering event of the XAML engine:

```C#
using Windows.UI.Xaml.Media;

this.InitializeComponent();
CompositionTarget.Rendering += CompositionTarget_Rendering;
...

private void CompositionTarget_Rendering(object sender, object e)
{
  myLineGraphCanvas.UpdateValues(new double[]
  {
      Value_1,
      ...
      
      Value_N
  });
}
```

#### With DispatcherTimer

Using a Timer class and set its Tick event:

```C#
this.InitializeComponent();
DispatcherTimer timer = new DispatcherTimer();
timer.Interval = new TimeSpan(0, 0, 0, 0, 10); // Each 10 ms
timer.Tick += Timer_Tick;
...

private void Timer_Tick(object sender, object e)
{
  myLineGraphCanvas.UpdateValues(new double[]
  {
      Value_1,
      ...
      
      Value_N
  });
}
```

You can use the Zoom In/Zoom Out buttons to update the Line Graph scale in real time.

## Example

You can see a working example of this control in the **MSBandViewer** application, [available here](https://github.com/niuware/MSBandViewer).

## Author

This application was coded by Erik Lopez.

## License

Licensed under [MIT License](https://github.com/niuware/LineGraphCanvas/blob/master/LICENSE)

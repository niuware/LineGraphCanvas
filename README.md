# LineGraphCanvas
===
*LineGraphCanvas* is a control for drawing line graphs in any Universal Windows Platform app.

## Usage

Simply add the control to the desired Page.xaml file as follows:

```Xaml
<LineGraphCanvas x:Name="myLineGraphCanvas" XScale="10.0" YScale="1.0" />
```

Then in the constructor of your Page.cs, initialize the LineGraphCanvas class adding as many lines as you need to represent in the graph:

```C#
this.InitializeComponent();
...

myLineGraphCanvas.Label = "My Graph Label";
myLineGraphCanvas.AddLineGraph(0.0, "Value Label", new SolidColorBrush(Windows.UI.Colors.XXX));
...
myLineGraphCanvas.AddLineGraph(0.0, "Other N Value Label", new SolidColorBrush(Windows.UI.Colors.XXX));
```

For the drawing loop you can choose between:

####CompositionTarget.Rendering 

Use the rendering event of the XAML engine as follows:

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

####DispatcherTimer

Or any other Timer class and set its Tick event to update the graph:

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

##Author

This application was coded entirely by Erik Lopez.

##License

Licensed under [MIT License](https://github.com/niuware/LineGraphCanvas/blob/master/LICENSE)

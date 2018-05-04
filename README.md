# WPF and XAML Practice

Hi Orien and friends. I wanted to quickly leave you with some of my thoughts on this project as it's important, in the interview process, for you to understand how I approach problems.

# Lecture Notes

## Introduction
### Why WPF?
**Windows Forms** is old. GDI/GDI+ was introduced in 1985 and doesn't play nice with modern GPUs.

**WPF** is based on ***DirectX*** and we can use it to build a rich UI that's compatible with modern GPUs. DirectX is a ***3D pipeline***.

 - Integrated tech for modern app building.
 - Vector graphics and, therefore, resolution independence.
 - Separation of programming and design.
 - Tons of customization, easy to stylize.

### WPF Architecture and Components

 - Kernel
	 - Video driver is managed as the kernel level.
 - Unmanaged
	 - DirectX sits on that. We don't manage this.
	 - MIL, the Composition Engine
		 - Manages complex shapes.860-805-5632
 - Managed
	 - Presentation Core
		 - Built on the MIL layer.
		 - We don't really work with this.
	 - Window Base
		 - Dependency object.
		 - Dispatcher.
	 - Presentation Framework
		 - Control, style, data bindings.

### WPF in 2015
Is it dead? No.
 - WPF Local
	 - WPF can be deployed separately from the .NET framework.

### .NET and WPF
 - WPF is part of the closed .NET Framework (then 4.6).
 - It's not part of .NET Core 5.

#### Universal Windows App Platform vs. WPF
UWP is cross-platform in the Windows ecosystem. WPF is Windows only. However, knowing WPF will make it easier to understand UWP.

### WPF Tools
 - Microsoft Blend
	 - Interactive tool.
	 - Sophisticated designs and layouts.
	 - More GUI based, used to create the GUI.
	 - Consistent look/feel with Visual Studio.
		 - Solution Explorer
		 - IntelliSense
		 - XAML navigation.
 - Visual Studio
	 - Coding, debugging experience.
	 - Timeline performance tool.
		 - What are my threads doing?
	 - Improved debugging of bindings and visual trees.

### UI Basics

 #### DPI
 - Dots per inch.
 - Only for printing.
#### PPI
 - Pixels per inch.
 - Monitors have pixels.
 - A measure of density.
 - A physical point in a raster image.

#### Raster Image

 - Grades of pixels.
 - The more pixels, the better the quality.
 - Better for fonts and other complex graphics that don't need to be scaled, or feature images for different resolutions.
 -
 #### Vector Image
 - Mathematical representation of an image.
 - Lines, border lines, polygons, ellipses, circles, etc.
 - These shapes are described in vector image files.
 - Can be scaled up without a loss in quality.
 - Harder to create complex graphics in vector format.
 - Small vector images can look bad.
 - Better for type setting or graphic design.
 - ***WPF renders Vector Images!***

	 #### Scaling
		1 logical unit = 1/96 inch
	 #### Aspect Ratio
	 #### ClearType Rendering

#### WPF Text Rendering
 - TextOptions.TextFormattingMode
	 - Ideal: If font > 14 pts.
	 - Display: If < 14 pts.
 - TextOptions.TextRenderingMode
	 - Auto
	 - Aliased
	 - Grayscale
	 - ClearType

### XAML Basics
#### Extensible Application Markup Language
 - Declarative Language
 - Similar to HTML
 - Window Properties
	 - Class
		 - We see that Window is derived from Main Window.
	 - Name Spaces
		 - xmlns
		 - xmlns: x
			 - For elements.
		 - xmlns: d
			 - Design Height
			 - Design Width
			 - Other design attributes.
		 - xmlns: mc
			 - Defining ignorable name spaces.
		 - xmlns: local
	 - We can access these properties using instances of Window as well.

 We can use either XAML or C# to construct these objects.

 #### Construction Flow
 - Object created.
 - Properties applied.
 - Event handlers attached.

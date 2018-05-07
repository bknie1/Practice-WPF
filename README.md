# WPF and XAML Practice
This is my study space for all things WPF .NET; from the basics to WPF with regards to the MVVC pattern.
# Lecture Notes
## Table of Contents
 1. [Introduction](#Introduction)
 2. [Controls](#Controls)
 3. [Layout](#Layout)
 4. [Properties and Events](#PropertiesandEvents)
 5. [Data Binding](#DataBinding)
 6. [Resources](#Resources)
 7. [Styles, Triggers, Templates, Skins](#StylesTriggersTemplatesSkins)
 8. [User Controls and Custom Controls](#UserControlsandCustomControls)
 9. [WPF Application Model](#WPFApplicationModel)

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

## Controls
![](https://4.bp.blogspot.com/-FSsPICI9wb0/TgIqtcQg34I/AAAAAAAAAEo/DBLnAe1CcvQ/s1600/WPF+Class+Hierarchy.PNG)

 - Framework elements are for data, styles.
 - ContentPresenter
	 - Placeholder for controls.
 - Controls
	 - Controls don't have appearance. They can be stylized, but on their own, they are strictly behavioral.
	 - Button Controls
		 - Button
			 - Click event fires after mouse button release.
		 - Repeat Button
			 - Fires on button down, for as long as its held down; it repeats.
		 - Toggle Button
			 - Check
			 - Radio
	 - Headered Content Control
		 - Expander
			 - Expands and collapses content.
			 - Toggled.
				 - isExpanded?
		 - GroupBox
			 - Visual, boxed grouping.
	 - Range Controls
		 - Slider
		 - ProgressBar
			 - Value set internally, via code.
		 - ScrollBar
	 - Items Controls
		 - ***ComboBox***
			 - A drop down list of items.
			 - *ItemsSource*
				 - Property that populates list using items from a specified source.
			 - We can explicitly add items to the combo box or dynamically using a source.
				 - Example
					 - Given explicit dates, we can use the property DisplayMemberPath and value "DayOfWeek" to replace dates with the appropriate day of the week for those dates.
				 - Items can be associated with different values.
					 - In the above example, selecting the date could yield a day of the week value.
			 - IsEditable and IsReadOnly can be enabled to allow searching. You don't want one without the other else search entries may create additional list items.
			 - You can make searching more granular by also using TextSearch.Text to assign explicit search values to items. e.g. Martin could be Uncle Bob's first name.
		 - ListBox
			 - A list of items with a scroll bar.
		 - TabControl
			 - Multiple tabs.
		 - TreeView
			 - Expand/Collapse
		 - Selectors
			 - Selectors allow selection of indexed items.
				 - Item, Index, Value, ValuePath.
		 - Images
		 - Menus
			 - DockPanel -> StatusBar and StackPanel -> Menu -> Menu Item
 - Shapes
 - Panels
	 - Canvases, grids, and other organizational elements.

## Layout
### Layout Core Types

 - UIElement
	 - Measure
		 - Recursive process.
		 - Each UIElement has a DesiredSize. It asks its children how much space it wants to encompass.
	 - Arrange
 - FrameworkElement: Sizing, positioning.
	 - Height
	 - Width
	 - HorizontalAlignment
	 - VerticalAlignment
 - Panel
	 - Base class for all panels.

### Layout Process

 1. Each UI element determines its DesiredSize.
 2. Assign sizes and positions.
 3. Render the scene.

## Properties and Events
### Dependency Properties

 - Ordinary .NET properties wrap Dependency Properties.
 - Stored in optimized pool.
 - AttachedProperty can be added to any applicable elements.
	 - Data binding.
	 - Default values.
	 - Styling, animation.
	 - etc.

### Routed Events
#### Three Types
 - Tunneling
 - Bubbling
 - Direct Events

#### Tunneling
Highest level reacts first, then tunnels down.
*Window -> Panel -> Rectangle*
#### Bubbling
Lowest level reacts first, then bubbles up the tree.
*Rectangle -> Panel -> Window*
#### Direct Events
We access the event directly.
*Rectangle*

## Data Binding

 - The target of a binding should be a **DependencyProperty**.
 - Any object can be the source of data.

### Basics
#### Properties
 - Source: Defines source object.
 - Path: Defines path to source property.
	 - e.g. Source can point to a student, but path can get its name property.
 - ElementName: Refers to named UI elements in the tree.
 - Mode
	 - OneWay
	 - TwoWay
	 - OneWayToSource
	 - Default: Depends on the element. Good practice to specify, though.

#### GUI Slider and TextBox Binding Example

 - Slider object has a value property.
 - To data bind, we say Value="{ Binding ElementName=ValueText", Path=Text, Mode=TwoWay }
 - Now, the text box reflects the value of the slider.
	 - This example is not optimized. Instead, we can use a delay to simulate periodic updates.
 - We can reverse this example and have the text box value update the slider's position.
	 - We can use UpdateSourceTrigger to define an event. By default, for textbox, it is tab. We can specific enter, or PropertyChanged, or other inputs.
 - StringFormat property can be used to define a format. e.g. F2 = hundredths floating point (0.00).

### Source Object

 - ElementName: Defines source in visual tree.
 - RelativeSource: Similar, but provides special features for searching for UI elements.
 - DataContext: Sets source as a context for many elements.
 - Source: Defines a source object by referencing it via the StaticResource extension.

#### Model Data Binding Example (C#)
 - We create an instance of Craftsman; he has a name, age, and picture.
 - We instantiate a new Binding for each property of our Craftsman.
	 - ageBinding = new Binding();
	 - ageBinding.Source = Craftsmen
	 - ageBinding.Path = new PropertyPath("Age");
	 - etc.
 - We can create this binding in either C# or XAML. **However, by default, XAML doesn't have access to specific instances of an object**. See below.

#### Model Data Binding Example (XAML)
In XAML, we can create a View that receives a ViewModel with Model information. That way, our View can reference this.Model's data; similar to razor views in ASP .NET.

 - Creating an instance of Window.Resources, we can access an instance of the model.
 - In Window, we can use the DataContext property to indicate that all children should be able to access this.data. That way, we don't have to initialize that resource wherever we use it; we initialize it locally in the window's entire scope.
	 - We can do this in the specific element only, as well.

This way, we can remove this bind logic from the model itself and instead keep it in the View. Then, we only have to pass an appropriate model to the view, instead of specific data from that model.

### Changes Notification
Without a Changes notification, the UI won't receive updates if the user changes/updates object information.

#### Binding to an Object Example
 - We have to create an interface for our existing model.
	 - e.g. Craftsman : INotifyPropertyChanged
		 - Rather than *just* craftsman.
 - The [NotifyPropertyChangedInvocator] annotation features a virtual method that, OnPropertyChanged, updates the visual representation of our data.
	 - Note: ReSharper can help generate these methods for us!

#### Binding to a Collection Example
We can use this to populate our UI with a series of items, rather than just one. We can use templates to format these items. Note: Lists are not compatible with collection binding. Instead, we use observable collections.

### Data Grid
This is the most powerful, complex, and confusing control system. It's essential for data binding because it will **auto-generate** as many grid columns as we need for each property of an object.

***This is likely the most important control in WPF!***

DataGrid generates columns of the following types according to the binding property source types:

 - TextBox columns for string values.
 - CheckBox columns for boolean values.
 - ComboBox columns for enunerable values.
 - Hyperlink columns for Uri values.

 #### Column Properties
 - CanUserReorderColumns
 - CanUserResizeColumns
 - CanUserResizeRows
 - CanUserSortColumns

### Converters
Bridge between incompatible types of targets and sources.

#### IValueConverter
 - Convert(object value, Type targetType, object parameter)
 - ConvertBack(object value, Type targetType, object parameter, CultureInfo culture))

#### Asnychronous Bindings
 - Bindings work with data in the UI thread by default.
 - ***Very easy to implement***.
 - In the property you want to make asynchronous:
	 - Set **IsAsync** to **true**.
	 - Gets/Sets under the hood.
	 - Usually that is all you have to do.

## Resources
### Binary Resources
 - Refers to binary streams.
 - Files
 - You can set a build action.
	 - Content: Loose resource on the disk.
		 -  It will stay as a loose file in the disk and acquired at run-time.
	 - Resource: Embedded in assembly, extended WPF support.
		 - At first, treated similarly to content.
		 - However, this is embedded in the assembly of the project.
	 - Embedded Resource: Embedded in assembly.
	 -
### Logical Resources
 - For ...
	 - Styles
	 - Templates
	 - Graphics
	 - Brushes
	 - .NET Objects
 - Frameworkelement and FrameworkContentElement
 - Use ResourceDictionary
	 - Lazy initialization; the software won't fetch the resource until it's needed during run-time. Less initial overhead.
 - Logical resources defined and referenced in XAML.

### Static Resource Extensions
Cannot be changed during run time. At compile time, refers to one specific instantiation of an object.

### Dynamic Resource Extensions
Can be changed during run time. The object can be re-instantiated as something else.

### Resource Lookup Algorithm

 1. Try to find resource in current element's resource dictionary.
 2. Not found? Check each parent until we reach the root.
 3. Not found? Check the application scope.
 4. Not found? Check the system theme.
 5. Not found? Check the system itself.
 6. Still not found? Throw InvalidOperationException.

### Resource Dictionaries
Resource dictionaries can be placed into separate XAML files. They are usually divided by Control types.

***Note: In order to make these dictionaries visible they have to be merged in the application scope.***

#### How?
In application resources (App.xaml) we can create an element, ResourceDictionary, with another element, ResourceDictionary.MergedDictionaries, and list ResourceDictionary elements that path to each of our separate dictionaries.

## Styles, Triggers, Templates, Skins
 - Styles enhance the look of WPF applications. They can be applied multiple times.
 - Triggers make styles, templates, and bindings reactive.
 - Templates help change the look of controls.
 - Skins change the look of a WPF application on the fly.

### Styles
Declared as a Resource. We can use the key (name) to apply this style to our XAML elements (much like CSS is applied to HTML).

### Triggers
 - Property Trigger: Applied when a dependency property becomes equal to an expected value defined in a trigger. Add/removing styles.
	 - e.g. \<Trigger> Property="IsMouseOver" Value="True"
		 - \<Setter Property="Foreground" Value="Red"/>
 - Data Trigger: Same as Property Trigger, but works with plain .NET properties.
	 - \<Style TargetType="{x:Type TextBox">
		 - <Style.Triggers>
			 - \<DataTrigger Binding=" { ... Path=Text.Length}" Value="3">
				 - \<Setter Property="Foreground" Value="Red"/>
				 - If the text length > 3, apply style.
 - Event Trigger: Applied when a specific event has been raised.
	 - e.g. RoutedEvent="MouseEnter"

### Templates
 - Controls are based on templates. You can use templates to re-style without compromising functionality.
 - Templates define a key and target type.

### Skins
 - Change the appearance of an application during runtime.
 - Supported by a mix of resource, style, and template systems in WPF.

## User Controls and Custom Controls
#### User Controls
User controls are reusable, composed, and have interconnecting logic. They are comprised of existing controls. It's more like a partial view in ASP.

 #### Custom Controls
 Custom controls are separate; buttons, progress bars. You only need these when there isn't a default user control that can do the job. This is a complex topic and may even be someone's specialization.

## WPF Application Model
### App.xaml and Visual Studio Project Dependencies
Don't mess with App.xaml. Visual Studio needs this to stay organized.

### Startup and Shutdown
We can still override initialization and shutdown sequences as long as we call startup args and make sure the overrides are fully written.

### Threading Model
#### STA: Single Threaded Apartment
STA means UI elements have thread affinity. The thread that creates a UI element becomes the owner. Only the owner can interact with that element directly.

All WPF UI elements are derived from the dispatcher object.

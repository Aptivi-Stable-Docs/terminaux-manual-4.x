---
description: Drawing geometric shapes to the console!
---

# 💠 Geometric Shapes

Terminaux also provides a wide assortment of classes that allow you to render different geometric shapes to the console easily. You can select one of the following shapes to render to your console:

* Rectangle
* Square
* Triangle
* Trapezoid
* Parallelogram
* Circle
* Ellipsis

They implement the `IGeometricShape` interface to allow you to iteratively render different geometric shapes from arrays of shapes that you can loop through to speed up the process and to allow you to implement your custom geometric shape.

To render a geometric shape, such as a rectangle, to the console, you must create a new instance of a shape class, providing the width and the height of the shape, as well as the position that tells Terminaux where to render the shape, whether to render the outline or the full shape (optional), and the selected color (optional).

{% hint style="info" %}
It's up to your shape class to have a constructor that doesn't necessarily require all the shape arguments as outlined above.
{% endhint %}

After creating a new instance, just call `Render()` on the shape instance.

{% code title="RenderRectangle.cs" lineNumbers="true" %}
```csharp
var rect = new Rectangle(15, 5, 4, 2, true, ConsoleColors.Red);
var rect2 = new Rectangle(15, 5, 21, 2, false, ConsoleColors.Aqua);
TextWriterRaw.WriteRaw(rect.Render());
TextWriterRaw.WriteRaw(rect2.Render());
```
{% endcode %}

<figure><img src="../../.gitbook/assets/image (1).png" alt=""><figcaption></figcaption></figure>

For general graphics tools, it provides the following functions found in the `GraphicsTools` class in the `Terminaux.Graphics` namespace:

* `RenderLine()`: Renders a colored line using the [Bresenham's line algorithm](https://en.wikipedia.org/wiki/Bresenham's\_line\_algorithm).
* `RenderLineSmooth()`: Renders a colored anti-aliasedline using [Xiaolin Wu's line algorithm](https://en.wikipedia.org/wiki/Xiaolin\_Wu's\_line\_algorithm).

{% hint style="info" %}
Rendering geometric shapes and lines require that you either buffer it to your [screen part](console-screen.md), or call the `TextWriterRaw.WriteRaw()` function, passing it the resultant string.
{% endhint %}

---
description: Presenting your things to the kernel!
---

# 📽️ Presentation System

This API provides you the presentation system used for presenting something to your users in the full-screen view. It's like a presentation in steroids.

## How to present

To present your presentation to your users, you must implement a `Presentation` class instance, which must assign the following variables in the constructor:

* `Name`
  * Presentation name
* `Pages`
  * Presentation pages (List of `PresentationPage` instances)

To implement the `PresentationPage` instances, you must call its constructor with the following variables:

* `Name`
  * Presentation page name
* `Pages`
  * Presentation page elements (List of `IElement` instances)

To implement the page elements, make new instances of the elements. Base elements that Nitrocid KS implements are:

* `TextElement`
  * Static text.
  * The first argument in the element `Arguments` is the string to be printed.
* `DynamicTextElement`
  * Dynamic text.
  * The first argument in the element `Arguments` is the action to which it generates the string, for example, `TimeDateRenderers.Render()`.

{% hint style="info" %}
You can also make your custom `IElement` in your code, and no registration is needed.
{% endhint %}

### Controls

The presentation viewer has the following controls:

* `ENTER` / `Left-click (mouse)`
  * Advances to the next page
* `ESC`
  * Bails out from the presentation
  * Has no effect on kiosk and modal presentations

### Input

In addition to the presentation elements, you can also add input to your presentation to interact with your users more. Just create a new instance of the `InputInfo` class and provide the title, the description, and a new instance of the input method class that implements the `IInputMethod` interface and the `BaseInputMethod` class.

```csharp
internal static InputInfo input =
    new("Second choice", "Asks the user to select one of the names (larger)",
        new SelectionInputMethod()
        {
            Question = "Ultricies mi eget mauris pharetra sapien et ligula:",
            Choices = data2.Select((data) => new InputChoiceInfo(data, data)).ToArray()
        }, true
    );
```

Then, in the `PresentationPage` constructor, you must add your input instance to the second argument that represents an array of `InputInfo` class instances, like this:

```csharp
new PresentationPage("Fifth page - Debugging choice input",
    [
        new TextElement()
        {
            Arguments = [
                "Tincidunt nunc pulvinar sapien et ligula ullamcorper malesuada proin."
            ]
        },
    ],
    [
        input2,
        input3,
    ]
),
```

{% hint style="info" %}
In order to be able to get the input, it's recommended to put the `InputInfo` instances in their own variables so that you can act according to the input value.

* `DisplayInput` corresponds to the displayed input that shows in the input selection box, and doesn't represent the actual input.
* `Input` represents the actual input, and the return type is determined by the generic `IInputMethod` interface and the generic `BaseInputMethod` class.

You can also specify whether the input is required in the `InputInfo` constructor. Currently, the input is not required, but you can pass `true` to the fourth argument to make it required, such as in the example above.
{% endhint %}

Making your input method class requires that you've already implemented the following in order:

* `BaseInputMethod` (generic): The base input method to simplify the implementation of your input method)
* `IInputMethod` (generic): The generic interface that specifies the return type of the input
* `IInputMethod` (base): The most basic interface that provides all the functions needed for input methods

Depending on your input method, you can at least override the following:

* `DisplayInput`
* `Input`
* `PromptInput()`: A method that prompts the user for the input, such as the color selector.
* `Process()`: A method that processes the input to validate it. True means that it's valid, and false means that it's invalid.

{% hint style="info" %}
You can override all the functions and the properties in the `BaseInputMethod` class, but be sure that you consider the use cases of your input method.
{% endhint %}

{% hint style="success" %}
There's no need for you to register your input method!
{% endhint %}

The presentation system checks the page to see if there are any input instances. If true, you'll be presented with an informational box telling you to select an input to fill. The asterisk next to the number denotes the required input. This means that users should fill in such input before being able to go on. Those without the asterisk means that it's fully optional.

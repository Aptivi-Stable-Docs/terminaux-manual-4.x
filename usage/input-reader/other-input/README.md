---
description: Other input...
---

# ✍️ Other Input

Terminaux not only provides the normal input reader with its custom bindings and its customizability, but you can also use its other input functions, such as informational boxes.

Terminaux currently provides the following input styles:

* Choice (one line, two lines, modern, and table)
* Info box (buttons, normal, input, password input, progress, slider (with minimum, current, and maximum values), selection, and multiple choices)
* Selection (single choice, multiple choices)

In addition to the three styles, you can also consult the following additional and specialized styles:

{% content-ref url="figlet-font-selector.md" %}
[figlet-font-selector.md](figlet-font-selector.md)
{% endcontent-ref %}

{% content-ref url="color-wheel.md" %}
[color-wheel.md](color-wheel.md)
{% endcontent-ref %}

The selection style contains a settings argument that you can easily make a class instance out of it, called `SelectionStyleSettings`. This class contains a singleton property that serves as a global settings for the selection input settings. This class currently contains the following color settings:

* Question
* Slider
* Input
* Option
* Alternative Option
* Selected Option
* Disabled Option
* Separator
* Text

{% hint style="info" %}
Here are some tips that apply to selection style inputs:

* The overloads that contain a settings argument let you pass your custom settings to the current selection style invocation, while the overloads that don't contain this parameter use the global settings.
* In multiple choice selections, you can press `A` to select all the choices. You can also press `F` to initiate a case-insensitive search for long choice selections to point you quickly to the desired choice.
* To enable or disable page counter indicator (to show or hide it), press `C`.
{% endhint %}

All input choices use the `InputChoiceInfo` array to define the choices. Not only do they indicate choices, but they also contain some settings, such as the default selection position, default selection indicator (like a checkbox, checked or not), and disabled option.

* `ChoiceDefault`: Indicates whether the choice instance is a default choice or not. All input handlers should select the first instance with this variable set to true as a default choice. Disabled choices can't be a default choice at the same time.
* `ChoiceDefaultSelected`: Indicates whether this choice instance is ticked or not (as in multiple selection, such as checkboxes). Disabled choices can set this as enabled.
* `ChoiceDisabled`: Indicates whether the user can not interact with this choice (select or tick it).

{% hint style="danger" %}
All input must require that at least one of the choices is enabled by default. Otherwise, an exception will be thrown.
{% endhint %}

If you want to obtain the `InputChoiceInfo` array, you can use the `InputChoiceTools` class to be able to use either a set of answers as a single string delimited by the slash character, such as Y/N/C, or an array of answers. Their titles can be optionally defined, but they will be numbered if either the answers or the titles are missing.

Below functions will help you get an array of `InputChoiceInfo`:

* `GetInputChoices((string, string)[] Answers)`
* `GetInputChoices(string[] Answers)`

{% hint style="info" %}
You can use this output to define choices while calling the above input functions.
{% endhint %}

Additionally, if you want to render the selection panel, you may want to use the `SelectionInputTools` class the contains the `RenderSelections()` function with the following arguments:

* List of selections
* Zero-based left and top position for the upper left corner
* Current selection index
* (optional) List of zero-based current selection numbers (for multiple choice selection)
* One-based count of choices to be displayed in a single panel
* Width of the selection panel
* (optional) Whether to render the slider inside or outside
* (optional) Alternate choice position (zero-based) that is a marker for the start of the alternate choice
* (optional) Whether to swap the selected choice color or not
* (optional) Selection element colors

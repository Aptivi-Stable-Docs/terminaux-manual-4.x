---
description: We need to write to the console
---

# 🖊️ Console Writers

Terminaux provides a vast amount of console writers for different purposes, like the progress bar writer, writing console output in color, etc. Also, you can use their `Render()` functions found in basically every static writer (not those that are dynamic, such as wrapped writers).

{% hint style="info" %}
The `Render()` functions are made primarily for plain writing operations. You can use them with `TextWriterRaw` writers.
{% endhint %}

## Standard console writers

The standard console writers provide you with non-moving parts of the text. They have their own writers and renderers to allow you to use them in two ways. The writer writes directly to the console, while the renderers are more suitable for the screen feature that you can check out at:

{% content-ref url="console-screen.md" %}
[console-screen.md](console-screen.md)
{% endcontent-ref %}

### Normal console writers

Starting from `ConsoleWriters`, this namespace provides the following classes:

* `ListWriterColor`
  * Provides you with the necessary functions to let you write the list entries to the console easily. It supports both non-generic and generic enumerables and dictionaries.
* `TextWriterRaw`
  * Provides you with the necessary functions to allow you to write the raw text to the console either to the standard output or the standard error.
* `TextWriterColor`
  * Provides you with the necessary functions to allow you to write the text to the console with and without color.
* `TextWriterHighlightedColor`
  * Provides you with the necessary functions to allow you to write the highlighted text to the console with and without color.
  * By default, the modern way of highlighting specific text is enabled by using a VT sequence intended to reverse the colors. If you still want to use the legacy way, you'll have to set the `legacy` argument to `true` before passing in all the usual parameters.
* `TextWriterWhereColor`
  * Provides you with the necessary functions to write the text in a specific position to the console with and without color.
* `RainbowTextWriterColor`
  * Provides you with the necessary functions to write the text with a rainbow colors spread around the text as foreground color.
* `RainbowBackTextWriterColor`
  * Provides you with the necessary functions to write the text with a rainbow colors spread around the text as background color.

Consult the below page to find out how to use these functions.

{% embed url="https://aptivi.github.io/Terminaux/api/Terminaux.Writer.ConsoleWriters.html" %}

{% hint style="info" %}
The console writers have three variants of writing functions:

* `Write()`: Default colors
* `WriteColor()`: Foreground colors
* `WriteColorBack()`: Foreground and background colors
{% endhint %}

#### Wrapped pager controls

The below wrapped pager controls are available when wrapping is enabled:

* `ESC`: Exits the pager
* `Page Up`: Moves the output by one page backward, but stops at the beginning of the output.
* `Page Down`: Moves the output by one page forward, but stops at the end of the output.
* `Up Arrow`: Moves up by one line
* `Down Arrow`: Moves down by one line
* `Home`: Goes to the first page
* `End`: Goes to the last page
* `Any key`: Moves the output by one page forward and exits if it reaches end of line

### Fancy writers

Alongside these writers, there are also writers that are categorized as "fancy" because they either print so awesome or they print graphics. Some of these writers allow you to supply text and/or a title. They can be found in the `FancyWriters` namespace that provides the below classes:

* `BorderColor`
  * Provides you with the necessary functions to allow you to draw a border somewhere in the console and with colors (border, background, and text).
* `BorderTextColor`
  * Provides you with the necessary functions to allow you to draw a border somewhere in the console with text inside the box and with colors (border, background, and text).
* `BoxColor`
  * Provides you with the necessary functions to allow you to draw a box somewhere in the console.
* `BoxFrameColor`
  * Provides you with the necessary functions to allow you to draw a box frame somewhere in the console and with colors (border, background, and text).
* `CenteredFigletTextColor`
  * Provides you with the necessary functions to allow you to render a string using the provided Figlet font in the middle of the console.
* `CenteredTextColor`
  * Provides you with the necessary functions to allow you to render a string in the middle of the console.
* `FigletColor`
  * Provides you with the necessary functions to allow you to render a string using the provided Figlet font to the console.
* `FigletWhereColor`
  * Provides you with the necessary functions to allow you to render a string using the provided Figlet font to the console at any position you want.
* `InfoBoxColor`
  * Provides you with the necessary functions to allow you to render an information box containing text inside it in the middle of the console. You can make it either modal (having a user press any key to exit) or informational (not waiting for any user input).
* `PowerLineColor`
  * Provides you with the necessary functions to allow you to build PowerLine segments and display them to the console.
* `ProgressBarColor`
  * Provides you with the necessary functions to allow you to render a horizontal progress bar to the console.
* `ProgressBarVerticalColor`
  * Provides you with the necessary functions to allow you to render a vertical progress bar to the console.
* `SeparatorWriterColor`
  * Provides you with the necessary functions to allow you to render a separator including text to the console.
* `TableColor`
  * Provides you with the necessary functions to allow you to render a table to the console.
* `SliderVerticalColor`
  * Provides you with the necessary functions to allow you to render a vertical slider to the console. The `Absolute` versions of the functions are generally easier to use than the normal ones, because they describe ranges as actual numbers rather than the slider console cells.
* `SliderColor`
  * Provides you with the necessary functions to allow you to render a horizontal slider to the console. The `Absolute` versions of the functions are generally easier to use than the normal ones, because they describe ranges as actual numbers rather than the slider console cells.

Consult the below page to find out how to use these functions.

{% embed url="https://aptivi.github.io/Terminaux/api/Terminaux.Writer.FancyWriters.html" %}

The tools for fancy writers can also be found here:

{% embed url="https://aptivi.github.io/Terminaux/api/Terminaux.Writer.FancyWriters.Tools.html" %}

### Miscellaneous writers

Finally, the miscellaneous writers are the writers that don't have any meaningful category. That's when `MiscWriters` comes in. This namespace contains these classes:

* `TextWriterSlowColor`
  * Provides you with the necessary functions to simulate a typewriter writing a requested string to the console with and without color.
* `TextWriterWhereSlowColor`
  * Provides you with the necessary functions to simulate a typewriter that writes a text in a specific position to the console with and without color.
* `TextWriterWrappedColor`
  * Provides you with the necessary functions to allow you to wrap long outputs to pages, also called a pager.
* `KeybindingsWriter`
  * Provides you with the nececssary functions that allow you to write the horizontal list of keybindings according to the list specified.

Consult the below page to find out how to use these functions:

{% embed url="https://aptivi.github.io/Terminaux/api/Terminaux.Writer.MiscWriters.html" %}

## Dynamic writers

In addition to the standard writers, there exists dynamic writers that allow you to render moving parts of text to the console. This type of writers are usable only when writing to the console directly.

This namespace contains these classes:

* `LineHandleWriter`
  * Provides you with the necessary functions to allow you to render a line of a text file with the compiler-like line handle using the specified line and column to the console.
* `LineHandleRangedWriter`
  * Provides you with the necessary functions to allow you to render a line of a text file with the compiler-like line handle using the specified line and column range to the console. This is used to highlight relevant parts of the entire line

Consult the below page to find out how to use these functions:

{% embed url="https://aptivi.github.io/Terminaux/api/Terminaux.Writer.DynamicWriters.html" %}

## Miscellaneous

Some of the console writers allow customization, such as the bordered boxes or progress bars.

### Borders

You can customize the borders for some of the console writers that support borders by editing properties found in the global settings of the borders, which can be found in the `BorderSettings.GlobalSettings` property. You can pass your own instance of `BorderSettings` with your own customizations to the border and its properties to the supported writers and all the informational boxes. The following writers support editing the border settings:

* `BorderColor`
* `BorderTextColor`
* `BoxFrameColor`
* `ProgressBarColor`
* `ProgressBarVerticalColor`
* `SliderColor`
* `SliderVerticalColor`

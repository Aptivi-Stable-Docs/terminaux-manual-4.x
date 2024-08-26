---
description: How can you extend your console?
---

# ➕ Console Extensions

Terminaux not only provides basic console tools to make building your console applications easier, but you can also rely on the extensions provided below to maximize your productivity. Below are the extensions that you can use. Any extension that is not documented can be referred to in the API documentation below:

{% embed url="https://aptivi.github.io/Terminaux/api/Terminaux.Base.Extensions.html" %}

{% hint style="info" %}
Certain features in this section may not work for different terminal emulators. For such terminal emulators, you may see nothing changing or something completely different happening. Use this feature accordingly.

The demo of Terminaux provides tests for some of the extensions, so you can check your console for support.
{% endhint %}

## Cursor tools

The `ConsoleCursor` class contains extensions that allow you to change the cursor in the terminal, including making the cursor visible or hidden and changing the cursor shape. The following tools are available:

* `CursorVisible`: Specifies whether the cursor is visible or not.
* `CursorType`: Specifies the cursor type, like blinking or steady block, underscore, or vertical bar.

## Clearing the console

`ConsoleClearing` provides you with tools to ease clearing the console and resetting its state. You can use the following functions:

* `ClearLineToRight()`: Allows you to clear the line to the right using the current background color in the current position.
* `GetClearLineToRightSequence()`: Gets a sequence that clears the line to the right using the current background color in the current position.
* `ResetAll()`: Resets the entire console.
* `GetClearWholeScreenSequence()`: Gets a sequence that clears the whole display, including the scrollback buffer.

## Console positioning

In the `ConsolePositioning` class, you can manipulate with the cursor position in various ways, such as calling the below functions that do different things:

* `ClearKeepPosition()`: Allows you to clear the console and keep the cursor position.
* `GetFilteredPositions()`: Allows you to get the filtered positions (X, Y) after filtering the specified text from the VT sequence in the current cursor position by simulating write operation.

## Console formatting

The `ConsoleFormatting` class provides you with text formatting tools, including making the text bold, italicize it, and more. This affects all text that have been written to the console inside and outside Terminaux. Fortunately, we have two modes:

* Dry setting: You'll have to call the function `GetFormattingSequences()` in the text sequence that you want to write to any writer. After that, you'll have to reset the formatting by hand.
* Non-dry setting: You'll have to call the function `SetFormatting()` to affect all text writes. If you want to reset all formatting, you'll have to call `ResetFormatting()`.

{% hint style="info" %}
Your terminal emulator may not support all the formatting modes, so consult your terminal's manual to verify that all the formats supported by Terminaux are supported. Additionally, the Terminaux demo app provides a test facade, `TestFormatting`, that allows you to test your console for support of all the text formatting options.
{% endhint %}

## Console characters

You can also manipulate with the console characters using the following functions:

* `GetCharWidth()`
* `EstimateCellWidth()`
* `EstimateZeroWidths()`
* `EstimateFullWidths()`
* `GetCharWidthType()`

{% hint style="info" %}
Please note that this information doesn't indicate the string length either by the amount of UTF-8 characters or by the text element as `StringInfo` class returns. This indicates how many console grid cells a character or a sentence consumes.
{% endhint %}

## Miscellaneous console extensions

The following extensions that don't fit in any of the categories can be used in your applications:

* `SetTitle()`
* `PercentRepeat()`
* `PercentRepeatTargeted()`
* `FilterVTSequences()`
* `GetWrappedSentences()`
* `GetWrappedSentencesByWords()`
* `Truncate()`
* `ShowMainBuffer()`
* `ShowAltBuffer()`
* `IsOnAltBuffer`

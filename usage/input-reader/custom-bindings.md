---
description: How to assign your own binding?
---

# 🔌 Custom Bindings

TermRead supports custom bindings, which you can assign your `BaseBinding` class containing the following functions you must override:

* `BoundKeys`
  * This holds all the keys to bind your custom action to.
* `DoAction(TermReaderState)`
  * This is the heart of your key binding. You can do anything with the text using the current terminal reader state.

You can also override these:

* `IsExit`
  * If `true`, causes TermRead to assume that the input is done after executing the action that this binding implements.
* `BindMatched(ConsoleKeyInfo)`
  * Specify your own method on how to check to see if the input key matched all the bound keys (`BoundKeys`) in your custom key binding.
* `ResetSuggestionsTextPos`
  * Specifies whether to reset the text position saved for the suggestions. This is usually enabled for custom bindings that have to do with the suggestions.

## Principles

Your keybinding must follow the below principles:

* For text positioning, you must use any function in the `PositioningTools` class.
* For manual console manipulation, you must use any function in the `ConsoleWrapper` class.
* Your bound key must not be already bound to a key that was already bound by either a base or another custom binding, or two bindings execute at the same time, potentially causing conflict.
* To manipulate with text, you must use the `state.CurrentText` property. You must refresh the prompt thereafter.
* To refresh the prompt, you must use the `TermReaderTools.Refresh()` function.

At the end, your base class must look like this at minimum:

```csharp
using System;
using Terminaux.Reader;
using Terminaux.Reader.Tools;

namespace MyApp
{
    internal class MyBinding : BaseBinding, IBinding
    {
        public override ConsoleKeyInfo[] BoundKeys { get; } = 
        {
            // All keys listed below will lead to the below DoAction being executed.
            new ConsoleKeyInfo('\0', ConsoleKey.Key, false, false, false)
        };

        public override void DoAction(TermReaderState state)
        {
            // Your action.
            state.RefreshRequired = true;
        }
    }
}
```

where:

* `ConsoleKey.Key`
  * Any console key. Consult the [documentation](https://learn.microsoft.com/en-us/dotnet/api/system.consolekey) for more info.
* `\0`
  * A character that must match the corresponding `ConsoleKey.Key`.

{% hint style="info" %}
If you're assigning a key containing `CTRL`, you must assign a character number starting from `0x0`. For example, `CTRL+Y` is `\u0019`.
{% endhint %}

## How to bind

Once you created a base class as mentioned above, you can finally use the `BindingsTools` class to call the `Bind(BaseBinding)` function to add your own binding to the custom binding store, like this:

```csharp
BindingsTools.Bind(new MyBinding());
```

{% hint style="warning" %}
**Warning:** You must call this function once. It does nothing if your binding is already installed.
{% endhint %}

To remove binding, you must use the `Unbind(ConsoleKeyInfo)` command.

### Positioning tools

Your custom bindings can now change the cursor positioning when manipulating with text so that it becomes easier to make your custom bindings that use positioning tools.

Here are the functions you can use:

* `GoLeftmost()`: Changes the word position to the leftmost position, that is, the first letter.
* `GoRightmost()`: Changes the word position to the rightmost position, that is, the last letter.
* `GoForward()`: Changes the word position a step or a specified number of steps closer to the end of the text.
* `GoBack()`: Changes the word position a step or a specified number of steps closer to the beginning of the text.
* `SeekTo()`: Changes the word position to the selected zero-based position

Once you're done changing positions, if you need to verify that you've changed the position to the correct position, you can use the `Commit()` function.

{% hint style="info" %}
It's not necessary to use the `Commit()` function at the end of each custom binding, because the reader uses this function automatically based on whether to update the position or not.
{% endhint %}

### Writing tools

You can also append or remove a string in the `TermReaderTools` class. This means that you can either append text to the end of the input, insert text to the current position, or remove text from either the current position or from a specific character index from the input string. These are the functions that you can use:

* `GetMaximumInputLength()`
* `InsertNewText()`
* `RemoveText()`

## Writers

You can use the text writers with the current reader settings by using `TextWriterColor`'s `WriteForReader()` and its siblings, passing it the reader settings to take care of the margins.

## Conditionals

In addition to all the above features, you can also make your key binding beep under certain circumstances, such as if the current text position is at the start of the text and we're trying to move left, using one of the two conditional functions from the `ConditionalTools` class:

* `ShouldNot()`: Specifies that the specified condition should not be true
* `Should()`: Specifies that the specified condition should not be false

If either of these functions' assertions have failed, either your computer or your speakers emits a beep sound upon going back to the input mode.

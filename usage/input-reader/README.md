---
description: May I read what you've written, please?
---

# 📖 Input Reader

This functionality is an important part of any interactive console application, because it gives users a chance to input what they want to write to the console.

In case you want to listen to mouse events, you can consult the below page:

{% content-ref url="pointer-events.md" %}
[pointer-events.md](pointer-events.md)
{% endcontent-ref %}

In case you want to use something other than the reader, you can consult the other input tools defined in the below page:

{% content-ref url="other-input/" %}
[other-input](other-input/)
{% endcontent-ref %}

You can easily use this feature in any interactive console application that uses Terminaux. Just use the `Terminaux.Reader` class that contains the `Read()` functions and their overloaded versions.

{% hint style="info" %}
The reader not only provides the static text version for input prompts, but also the dynamic text version. Just create a simple function delegate that generates a string as the first argument, like this:

```csharp
string input = TermReader.Read(() => $"{DateTime.Now} [{TermReaderState.CurrentState.CurrentTextPos}]\n> ", "Hello World!", false, false, false);
```
{% endhint %}

{% hint style="info" %}
Please note that they are interruptible by default. If you want the input to be non-interruptible, you can set the `interruptible` argument to false.
{% endhint %}

Each one of these functions creates a reader state, `TermReaderState`, that contains essential information about the current reader state, including, but not limited to:

* Current text
* Input prompt text
* Current text position
* Kill buffer
* Reader settings

{% hint style="info" %}
If you're making your own mod in Nitrocid KS, it's best to use its own `Input` class instead of Terminaux's `TermReader`, as the class there actually deals with the screensaver in most circumstances.
{% endhint %}

Any key will append the selected characters to the current text input, and `RETURN` will accept the input. For more information about key bindings, go to the below page.

{% content-ref url="keybindings.md" %}
[keybindings.md](keybindings.md)
{% endcontent-ref %}

You can access the global reader settings by referencing the `GlobalReaderSettings` found in the `TermReader` class.

### History tools

You can now set the history entry list with your array of history entries or clear the history list using the following functions:

* `SetHistory(List<string> History)`
  * Sets the history to the chosen history list
* `ClearHistory()`
  * Clears all history entries

### State tools

You can also check to see if the console reader facility is busy getting input or not. The property, `Busy`, indicates this by returning `true` if there is input to be entered by the user.

{% hint style="info" %}
If you want to wait for user input to finish, you can call the `WaitForInput()` function in the `TermReaderTools` class.
{% endhint %}

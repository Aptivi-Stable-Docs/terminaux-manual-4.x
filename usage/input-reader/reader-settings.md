---
description: In case you want to set things up
---

# ⚙️ Reader Settings

The reader currently has a global settings instance session-wide. However, it can get overridden if you make a new instance of `TermReaderSettings` with some available properties mentioned below set. They get read each time you call this function or you activate a keybinding that uses one of these settings.

Here are the available settings that you can set:

* `PasswordMaskChar`
  * Sets the password masking character.
* `HistoryEnabled`
  * Whether the history is enabled or not.
* `HistoryName`
  * Select what history to use
* `LeftMargin`
  * Sets the left margin of the input.
* `RightMargin`
  * Sets the right margin of the input.
* `InputForegroundColor`
  * The foreground color for the input text, as well as the input prompt.
* `InputBackgroundColor`
  * The background color for the input text, as well as the input prompt.
* `Suggestions`
  * Sets a function that you could use to return an array of strings containing auto completion data.
* `SuggestionsDelimiters`
  * Delimiters to split the current input within a function that returns a list of suggestions.
* `TreatCtrlCAsInput`
  * Whether to treat `Ctrl` + `C` as input or not. If enabled, TermRead will process this keybinding as aborting the current input.
* `PlaceholderText`
  * This is the text that the terminal reader shows when there is no input text. This is used to give users hints on what they should write to the prompt.

{% hint style="info" %}
You can copy the above settings in one line using the overload of the `TermReaderSettings` constructor that allows you to specify another `TermReaderSettings` instance to copy the settings from that instance to the new one. This is useful if you want to use the global settings without affecting future reads. This is a simple example of how to copy the global settings and to set the password mask without affecting the global password mask:

<pre class="language-csharp"><code class="lang-csharp">// Doesn't affect future reads
<strong>var settings = new TermReaderSettings(TermReader.GlobalReaderSettings)
</strong><strong>{
</strong><strong>    PasswordMaskChar = '#'
</strong><strong>};
</strong>
// Affects future reads
TermReader.GlobalReaderSettings.PasswordMaskChar = '#';
</code></pre>
{% endhint %}

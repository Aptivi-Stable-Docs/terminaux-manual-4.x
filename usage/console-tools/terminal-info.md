---
description: What's your terminal type and its capabilities?
---

# 📟 Terminal Info

Terminal information database is a list of terminal capabilities that control how console applications determine capabilities in the terminal type that the emulator uses, such as the color depth capability and the method of writing sequences that change the background and the foreground color. Termcap was implemented in 1978, and Terminfo was implemented in 1981-1982. Applications that use `ncurses` (for non-C# applications) or Terminaux (for C# applications) can use the database to get the capabilities.

The TermInfo feature of Terminaux can be found in the base console tools namespace, `Terminaux.Base.TermInfo`.  `TermInfoDesc`'s functions contain the following:

* `TryLoad()`: Tries to load a terminal information description given the terminal type name.
* `Load()`: Loads a terminal information description given the terminal type name, and if the name is not given, it uses the current terminal type that your terminal emulator uses.
* `GetBuiltins()`: Gets a list of built-in terminal type names that Terminaux can find in the built-in capabilities list.

{% hint style="info" %}
This feature used to be exclusive to Linux users mostly, but we've added the built-in terminal information database so that Windows applications are now free to analyze such data, although `conhost` doesn't emulate any terminal.
{% endhint %}

Built-in terminal capabilities can be accessed as properties in the `TermInfoDesc` instance that the loading functions return when parsing the terminal information files. For extra properties that Terminaux doesn't cover, this class provides you with the following functions:

* `GetBoolean()`: Gets a boolean value that holds either true or false. Returns null, however, if Terminaux is unable to get the value.
* `GetNum()`: Gets a number value that holds a numeric integer. Returns null, however, if Terminaux is unable to get the value.
* `GetString()`: Gets a textual value. Returns null, however, if Terminaux is unable to get the value.

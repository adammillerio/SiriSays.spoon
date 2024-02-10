# SiriSays.spoon
SiriSays is a utility Spoon which provides a single function `siri` which can be used to submit text to Siri. There is also a provided alias that will allow you to send siri commands via the command line (see Usage).

This function is implemented as a "macro" which performs the following steps via the "Type-to-Siri" accessibility feature:

* Presses Fn+Space to open the Type-to-Siri (TTS) prompt
* Waits until "Notification Center" is the focused application (TTS prompt)
* Sends the provided prompt as keystrokes
* Presses return to submit prompt
* Waits typeToSiriCloseDelay seconds before "auto closing" the prompt
* Auto close focuses the window from before TTS prompt then clicks the center
  * Will not occur if prompt is already unfocused

To enable Type-to-Siri, set the following Settings on your macOS machine:
* Accessibility
    * Type to Siri
        * On
* Siri & Spotlight
    * Siri Responses
        * Voice Feedback
            * Off
        * Always show Siri captions
            * On
        * Keyboard Shortcut
            * Press Fn (Globe) Space

# Installation

SiriSays can be automatically installed from my [Spoon Repository](https://github.com/adammillerio/Spoons) via [SpoonInstall](https://www.hammerspoon.org/Spoons/SpoonInstall.html). See the repository README or the SpoonInstall docs for more information.

Example `init.lua` configuration which configures `SpoonInstall` and uses it to install and start SiriSays:

```lua
hs.loadSpoon("SpoonInstall")

spoon.SpoonInstall.repos.adammillerio = {
    url = "https://github.com/adammillerio/Spoons",
    desc = "adammillerio Personal Spoon repository",
    branch = "main"
}

spoon.SpoonInstall:andUse("SiriSays", {
    repo = "adammillerio",
    start = true
})
```

## Manual

Download the latest release from [here.](https://github.com/adammillerio/Spoons/raw/main/Spoons/SiriSays.spoon.zip)

Unzip and either double click to load the Spoon or place the contents manually in `~/.hammerspoon/Spoons`

Then load the Spoon in `~/.hammerspoon/init.lua`:

```lua
hs.loadSpoon("SiriSays")
hs.spoons.use("SiriSays", {start = true})
```

# Usage

The easiest way to use this is to leverage the Hammerspoon CLI (`hs`) to make a `siri` alias in your shell:

```bash
alias siri='hs -c "spoon.SiriSays:siri_cli(_cli.args)" --'
```

This can be used to invoke siri via natural language in the terminal:
```bash
siri turn on the living room lights
```

If you want to implement this macro in your own Hammerspoon configs, just load the Spoon and invoke `spoon.SiriSays:siri()` with your desired prompt string.

Refer to the [hosted documentation](https://adammiller.io/Spoons/SiriSays.html) for additional for information on usage.

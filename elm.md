# Elm

## Links
* [Elm homepage](http://elm-lang.org/)

## Installation
* See https://guide.elm-lang.org/install.html
* This basically says there's an [elm package in node](https://www.npmjs.com/package/elm)
* Global install: `npm install -g elm`

## Command Line
* `elm-repl` read eval print loop for Elm
* `elm-reactor` like `ng serve`, fires up a server at http://localhost:8000/
* `elm-make` builds/compiles your project to html or javascript
  * e.g. `elm-make Main.elm --output=main.html` 
* `elm-package` install/publish packages from/to the [elm package catalog](http://package.elm-lang.org/)

## Visual Studio Code Support
* See https://github.com/Krzysztof-Cieslak/vscode-elm
* Install this extension: https://marketplace.visualstudio.com/items?itemName=sbrink.elm
* About binding the elm.makeCommand
  * [These instructions](https://github.com/Krzysztof-Cieslak/vscode-elm) tell you to create a `.vscode/settings.json` file in the workspace root and add the following setting: `"elm.makeCommand": ".\\node_modules\\.bin\\elm-make"`
  * This is only needed when you installed Elm LOCALLY with `npm install --save-dev elm`
  * If you installed elm GLOBALLY, this is not needed and everything will just work out-of-the-box.
  * When you cobine the `elm.makeCommand` setting with a global install, you will start seeing the error `The system cannot find the path specified` on the first import statement.
* Features to remember
  * Enable `File, Auto Save` to let VSC autosave your elm files and get immediate error highlighting
  * Hover over a function to see signature and comment
  * Go to a function definition
    * Ctrl-click
    * F12
    * ALT-F12 for peeking
    * Also available in the context menu
  * Code actions
    * Click on the lightbulb (warning/error) to access code actions
    * Should also work with Ctrl+ but that triggers zoom on my laptop :-(
  * Elm commands
    * Ctrl-Shift-P for the command palette
    * type `elm`
    * all sorts of elm commands available (reactor, REPL, make, packages, ...)
  * REPL integration
    * ALT-: sends the current line to the REPL
    * ALT-ENTER sends the current selection to the REPL
  * Code completion
    * Ctrl-space
    * [Available snippets](https://github.com/Krzysztof-Cieslak/vscode-elm/blob/master/snippets/elm.json)
  * Formatting
    * Install https://github.com/avh4/elm-format but is still experimental
    * Then ALT-Shift-F of via command palette (Ctrl-Shift-P)

## Future Learnings
* [The Elm Architecture tutorial](https://guide.elm-lang.org/architecture/)
* [Time Traveling Debugger](http://debug.elm-lang.org/)
* [Elm Docs](http://elm-lang.org/docs)
* Tim Schraepen ASF live coding
  * [Twitch](https://go.twitch.tv/asf_livecoding/)
  * [Youtube channel](https://www.youtube.com/channel/UC-0Zos25VCU6h6bDiv7bh9w)

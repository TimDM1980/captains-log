# Elm

## Links
* [Elm homepage](http://elm-lang.org/)

## Setup
* [Install Elm](https://guide.elm-lang.org/install.html)
  * This basically says there's an elm package in node
  * https://www.npmjs.com/package/elm
  * `npm install -g elm`
* [Support for Visual Studio Code](https://github.com/Krzysztof-Cieslak/vscode-elm)
  * Install this extension: https://marketplace.visualstudio.com/items?itemName=sbrink.elm
  * Click `File, Auto Save` to autosave your elm files and get immediate error highlighting
  * About binding the elm.makeCommand
    * [These instructions](https://github.com/Krzysztof-Cieslak/vscode-elm) tell you to create a `.vscode/settings.json` file in the workspace root and add the following setting: `"elm.makeCommand": ".\\node_modules\\.bin\\elm-make"`
    * This is only needed when you installed Elm LOCALLY with `npm install --save-dev elm`
    * If you installed elm GLOBALLY, this is not needed and everything will just work out-of-the-box.
    * When you cobine the `elm.makeCommand` setting with a global install, you will start seeing the error `The system cannot find the path specified` on the first import statement.

## Commands
* `elm-repl` read eval print loop for Elm
* `elm-reactor` like `ng serve`, fires up a server at http://localhost:8000/
* `elm-make` builds/compiles your project to html or javascript
  * e.g. `elm-make Main.elm --output=main.html` 
* `elm-package` install/publish packages from/to the [elm package catalog](http://package.elm-lang.org/)

## Learn
* [The Elm Architecture tutorial](https://guide.elm-lang.org/architecture/)
* [Visual Studio Code extension features](https://github.com/Krzysztof-Cieslak/vscode-elm)
* [Elm Docs](http://elm-lang.org/docs)
* Tim Schraepen ASF live coding
  * [Twitch](https://go.twitch.tv/asf_livecoding/)
  * [Youtube channel](https://www.youtube.com/channel/UC-0Zos25VCU6h6bDiv7bh9w)

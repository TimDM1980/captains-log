# Elm

## Links
* [Elm homepage](http://elm-lang.org/)

## Setup
* [Install](https://guide.elm-lang.org/install.html)
  * This basically says there's an elm package in node
  * https://www.npmjs.com/package/elm
  * `npm install -g elm`
* Configure Visual Studio Code
  * [Instructions](https://github.com/Krzysztof-Cieslak/vscode-elm)
  * Install this extension: https://marketplace.visualstudio.com/items?itemName=sbrink.elm
  * Click File, Preferences, Settings and add `"elm.makeCommand": ".\\node_modules\\.bin\\elm-make"` to the user settings

## Commands
* `elm-repl` read eval print loop for Elm
* `elm-reactor` like `ng serve`, fires up a server at http://localhost:8000/
* `elm-make` builds/compiles your project to html or javascript
  * e.g. `elm-make Main.elm --output=main.html` 
* `elm-package` install/publish packages from/to the [elm package catalog](http://package.elm-lang.org/)

## Learn
* [The Elm Architecture tutorial](https://guide.elm-lang.org/architecture/)
* [Elm Docs](http://elm-lang.org/docs)
* Tim Schraepen ASF live coding
  * [Twitch](https://go.twitch.tv/asf_livecoding/)
  * [Youtube channel](https://www.youtube.com/channel/UC-0Zos25VCU6h6bDiv7bh9w)

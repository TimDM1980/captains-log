# Elm

## Links
* [Elm homepage](http://elm-lang.org/) - live examples, docs, community & blog
* An Introduction To Elm
  * [Online](https://guide.elm-lang.org/)
  * [GitBook](https://www.gitbook.com/book/evancz/an-introduction-to-elm/details)
* [Package Catalog](http://package.elm-lang.org/)
* [Local application](http://localhost:8000/) started with elm-reactor

## Installation
* Source: https://guide.elm-lang.org/install.html
* This basically says there's an [elm package in node](https://www.npmjs.com/package/elm)
* Global install: `npm install -g elm`
* Command Line
  * `elm-repl` read eval print loop for Elm
  * `elm-reactor` like `ng serve`, fires up a server at http://localhost:8000/
  * `elm-make` builds/compiles your project to html or javascript
    * e.g. `elm-make Main.elm --output=main.html` 
  * `elm-package` install/publish packages from/to the [elm package catalog](http://package.elm-lang.org/)

## Visual Studio Code Support
* Source https://github.com/Krzysztof-Cieslak/vscode-elm
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

## Core Language
* Source https://guide.elm-lang.org/core_language.html
* Source https://guide.elm-lang.org/types/
* string concat: `"hello" ++ "world"`
* integer division: `9 // 2` evaluates to `4`
* functions
  * function definition
    * `isNegative n = n < 0`
    * this function takes an argument `n` and checks that it is less than zero
  * function application
    * `isNegative 6`
    * use spaces instead of arguments in parentheses separated with commas
  * You can provide the type annotation yourself:
    * `isNegative : Int -> Bool`
    * Afterwards you can define the function: `isNegative n = n < 0`
    * REPL currently doens't support type annotations :-(
  * the arrow notation `->`
    * Describes the input and the output of a function
    * For example `String.length` can be described as `String -> Int`
    * It __must__ take a String and __must__ return an Int
    * If you apply this function and you don't give it a string, you get a compile error
    * what about multiple arrows???
      * `divide x y = x / y` is a `Float -> Float -> Float` function
      * The _easy_ way to grasp this, is to think that all the arguments are separated by arrows, and whatever is last is the result of the function
      * But ist's just __partial application__:
        * `divide x y = x / y`
        * `divide x = \y -> x / y`
        * `divide = \x -> (\y -> x / y)`
      * You can use functions like this as well, you don't have to give all the arguments at once :-)
        * `divide 128` evaluates to a `Float -> Float` function, which takes 1 argument and returns a Float
        * you can use the forward application operator `|>` to write `divide 128 2` as `2 |> divide 128`
  * Anonymous functions
    * Starts with a backslash, like `\n = n + 2`
    * To use it, wrap it in parentheses: `(\n = n + 2) 10` evaluates to `12`
    * You can even name them: `plusTwo = \n = n + 2`
    * If you throw away the backslash, you end up with the regular function definitions: `isNegative n = n < 0`
* `if True then "hello" else "world"`
  * No "truthiness" on non-boolean things
* Style
  * Start the body of a function on the next line
  * Syntax: next line must start with a whitespace!
  * REPL: use a backslash to split up lines
* Lists
  * `names = [ "Alice", "Bob", "Chuck" ]`
  * Similar to arrays in javascript
  * Values must have the same type
    * However, `[]` evaluates to a List with a type that is not specified yet
    * Since Elm embraces immutability, this plays out nicely:
      * `emptyList = []` is an empty list with no defined type
      * `listOfInts = 1 :: emptyList` gives a new list of ints
      * `"a" :: emptyList` gives a new list of strings
      * `"a" :: listOfInts` gives a compile error :-)
  * Lists library
    * `List.length names` evaluates to `3`
    * `List.map myFunction myList` applies `myFunction` to each element of `myList` and returns a new list
    * `List.::` add an element to the front of a list. Use it like this: `"Tim" :: names`
* Tuples
  * `(123, "a tuple with an int and a string")`
* Records
  * Set of key-value pairs, like objects in javascript, but
    * You cannot ask for a field that does not exist
    * No field will ever be undefined or null
    * You cannot create recursive records with a this or self keyword
  * `point = { x = 3, y = 4 }`
  * `bill = { name = "Gates", age = 57 }`
  * Access field using a dot: `point.x`
  * Use a field like a function
    * `.x point`
    * `List.map .name [bill, bill]` evaluates to `["Gates", "Gates"]`
  * Pattern matching
    * `under70 {age} = age < 70`
    * When you throw a record at this function, it will use its age property :-)
    * `under70 bill` evaluates to `True`
    * You can use any record, as long as it has an __age__ field that holds a __number__
    * Using `bill = { age2 = 57 }` gives a COMPILE error :-)
    * Using `bill = { age = "57" }` gives a COMPILE error :-)
  * Updating
    * `{ bill | name = "Nye" }`
    * __No destructive updates!__ We always return a new record

## The Elm Architecture
* [Tutorial](https://guide.elm-lang.org/architecture/)
* Clone the code at https://github.com/evancz/elm-architecture-tutorial/

## Future Learnings
* [Time Traveling Debugger](http://debug.elm-lang.org/)
* [Elm Docs](http://elm-lang.org/docs)
* Tim Schraepen ASF live coding
  * [Twitch](https://go.twitch.tv/asf_livecoding/)
  * [Youtube channel](https://www.youtube.com/channel/UC-0Zos25VCU6h6bDiv7bh9w)

# Elm Language

## Sources
* https://guide.elm-lang.org/core_language.html
* https://guide.elm-lang.org/types/
* https://guide.elm-lang.org/error_handling/

## Basics
* String concat: `"hello" ++ "world"`
* Integer division: `9 // 2` evaluates to `4`
* `if True then "hello" else "world"`
  * No "truthiness" on non-boolean things
* Tuples: `(123, "a tuple with an int and a string")`

## Functions
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
  * Use them with the List library: `List.filter (\x -> x > 0) listOfInts`
* Style
  * Start the body of a function on the next line
  * Syntax: next line must start with a whitespace!
  * REPL: use a backslash to split up lines

## Lists
* `names = [ "Alice", "Bob", "Chuck" ]`
* Type annotation for lists: `names : List String`
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

## Records
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

## Types    
* Type alias
  * Looks like Class definitions in Java
  * `type alias User = { name : String, bio : String, pic : String }`
  * You can use it for function in/output: `hasBio : User -> Bool`
  * Creating a type alias generates a record constructor: `User "Tom" "Friendly Carpenter" "http://example.com/tom.jpg"`
* Union types
  * Also called _tagged unions_
  * Looks like enums in Java
  * `type Visibility = All | Active | Completed`
  * Use them in case expressions: `case visibilityParam of All -> ...`
    * Important: Elm forces you to deal with all cases!
    * Otherwise, you get a compile error 
  * All those _values_ themselves are functions
    * You can see this more clearly here: `type User = Anonymous | Named String`
    * `Named` is a function that takes a String and returns a User, or `String -> User`
    * You can _instantiate_ it like so: `Named "Johnny"`
    * You can even access the String field: `case user of Named name -> "users/" ++ name ++ ".png"`
* Generic structures
  * Linked list: `type IntList = Empty | Node Int IntList`
  * Now you have recursion: `Node 64 (Node 128 Empty)`
  * You can think of recursive functions:
    ```
    sum numbers =
     case numbers of
      Empty ->
       0
      Node n remainingNumbers ->
       n + sum remainingNumbers
    ```
  * A generic linked list: `type List a = Empty | Node a (List a)`
  * A generic binary tree: `type Tree a = Empty | Node a (Tree a) (Tree a)`

## Error Handling
* Maybe
  * fixes null
  * `type Maybe a = Nothing | Just a`
  * A variable that can be _null_: `age : Maybe Int`
  * `age = Nothing` or `age = Just 24`
  * In case excpressions, we __have__ to deal with `Nothing`:
  ```
  canBuyAlcohol age =
    case age of
      Nothing ->
        False
      Just age ->
        age >= 21
  ```
  * List.filterMap drops items if you map function returns Nothing
* Result
  * fixes exceptions
* Task
  * fixes async exceptions
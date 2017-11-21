# The Elm Architecture

## Sources
* [Tutorial](https://guide.elm-lang.org/architecture/)
* Clone the code at https://github.com/evancz/elm-architecture-tutorial/

## Basic Pattern
* Model
  * the state of your application
  * `type alias Model = { propX : String, propY : String }`
  * this uses type alias, which is a bit like we would define a class
* Update
  * update the state
  * `type Msg = X | Y`
  * this is a union type, which looks a bit like an enumeration
  * ```
    update : Msg -> Model -> Model
    update msg model = 
      case msg of X -> { model | propX = "New X" }
      case msg of Y -> { model | propX = "New Y" }
    ```
  * this is an update function which takes a msg and a model and returns a new model
* View
  * view the state as html
  * ```
    view : Model -> Html Msg
    view model = ...
    ```
  * view takes your model and returns Html that can produce Msg values
    * "produce Msg values" sounds a bit weird, since syntactically it looks like Html is a function that "takes" a Msg...
    * Look at the definition: `type alias Html msg = VirtualDom.Node msg`
    * You're just filling in the type for the generic Html type alias
    * This is necessary because you defined the type Msg yourself

## Commands
* `update : Msg -> Model -> (Model, Cmd Msg)`
* update now returns a tuple: a Model and a Cmd _that can produce an Msg_
* 
  ```
  subscriptions : Model -> Sub Msg
  subscriptions model =
  ```
* now you can update your model indirectly:
  ```
  type Msg = Roll | NewFace Int

  update msg model =
    case msg of
      Roll -> (model, Random.generate NewFace (Random.int 1 6))

      NewFace newFace -> (Model newFace, Cmd.none)
  ```
* Roll doesn't update the model directly, it returns a Command that the Elm runtime will execute and the result will be that a NewFace message comes in, that will eventually update the model

## Subscriptions
* 
  ```
  subscriptions : Model -> Sub Msg
  subscriptions model = Time.every second Tick
  ```
* Every second, a Tick message is produced
* This will get picked up by the update method



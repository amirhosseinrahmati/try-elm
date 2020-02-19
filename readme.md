# Elm
#### Try At Least Once (JavaScript libraries and frameworks) > JavaScript Flavors > Elm

Official website: [https://elm-lang.org/](https://elm-lang.org/ "https://elm-lang.org/")

Github repository: [https://github.com/elm](https://github.com/elm "https://github.com/elm")

------------
## What is the Elm
Most of the [search results in Google](https://www.google.com/search?q=elm+language "search query results in Google") starts with this sentence: **Elm is a functional language that compiles to JavaScript**.
In Elm, most of the things you see is a function. Even minus - and plus + operators are functions.
> The fundamental principle of writing Elm code is to separate effects from computation and to use different techniques for each.
All computation is “pure”, meaning what a function returns depends only on its arguments. It’s predictable and easy to understand.

If you are used to programming in Java or JavaScript, the first thing you will see is the strange syntax in Elm which has no braces but has lots of arrows.

Elm compiler analyzes your to see how values flow through your program. The compiler shows error messages if values mismatch the types or used in an invalid way.

Elm made up of three concepts:
- **Model** — the state of the application
- **View** — a way to turn the state into HTML
- **Update** — takes messages and updates the state based on the content of the message

------------
### Installation
Visit [https://guide.elm-lang.org/install.html](https://guide.elm-lang.org/install.html "https://guide.elm-lang.org/install.html") to get the setup instructions. It's highly recommended especially for the functional language beginners, to use online editor and compiler of the Elm which is available at [http://elm-lang.org/try](http://elm-lang.org/try "http://elm-lang.org/try").

### Quick Example
This simple app almost clarifies the main concepts of the Elm language. There is a button which each time on the click event sends **Roll** message to the app then in the update section of the app, a function generates a random number between 1 to 100. New generated value returns to the view of the app.
```
import Browser
import Html exposing (..)
import Html.Events exposing (..)
import Random



-- MAIN


main =
  Browser.element
    { init = init
    , update = update
    , subscriptions = subscriptions
    , view = view
    }



-- MODEL


type alias Model =
  { dieFace : Int
  }


init : () -> (Model, Cmd Msg)
init _ =
  ( Model 1
  , Cmd.none
  )



-- UPDATE


type Msg
  = Roll
  | NewFace Int


update : Msg -> Model -> (Model, Cmd Msg)
update msg model =
  case msg of
    Roll ->
      ( model
      , Random.generate NewFace (Random.int 1 100)
      )

    NewFace newFace ->
      ( Model newFace
      , Cmd.none
      )



-- SUBSCRIPTIONS


subscriptions : Model -> Sub Msg
subscriptions model =
  Sub.none



-- VIEW


view : Model -> Html Msg
view model =
  div []
    [ h1 [] [ text (String.fromInt model.dieFace) ]
    , button [ onClick Roll ] [ text "Roll" ]
    ]
```
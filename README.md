# Elm, me gusta. :)

This is my personal note learning elm from ground up.

Learning curve:

1.  [Elm Programming](https://elmprogramming.com)

    1. Intro

       1. Why Elm?
       2. Feedback
       3. Who This Book is For
       4. Conventions Used in This Book
       5. Acknowledgement
       6. About the Author

    2. Getting Started

       1. Installation
       2. Building a Simple Web Page
       3. Elm Platform
       4. Elm Programming Language
       5. Elm Compiler
       6. Elm Architecture
       7. Elm Runtime
       8. elm make
       9. elm install
       10. elm reactor
       11. elm repl
       12. Ellie
       13. Conclusion

    3. Elm Language Basics

       1. Simple Arithmetic
       2. Boolean
       3. Comparison
       4. Comments
       5. Expression
       6. Value
       7. Constant
       8. If Expression
       9. Function
       10. Let Expression
       11. Case Expression
       12. Indentation
       13. String
       14. Regular Expression
       15. List
       16. Array
       17. Tuple
       18. Record
       19. Conclusion

    4. Benefits of Using Elm

       1. Immutability
       2. Pure Functions
       3. Solving Complex Problems with Simple Functions
       4. Easy to Test
       5. Type System
       6. Easier Code Organization
       7. Fuzz Testing
       8. Pattern Matching
       9. Conclusion
       10. Architecture
       11. Understand how the Elm Architecture helps us build robust front-end web applications

    5. Elm Architecture

       1. Model View Update - Part 1
       2. Virtual DOM
       3. Model View Update - Part 2
       4. Side Effects
       5. Commands
       6. Conclusion

    6. HTTP Requests

       1. Fetching Data Using GET
       2. Decoding JSON - Part 1
       3. Decoding JSON - Part 2
       4. RemoteData
       5. Retrieving Data on Initialization
       6. Conclusion

    7. Single-Page Apps

       1. What is a Single-Page App?
       2. Restructuring Code
       3. Creating Post Module
       4. Creating List Posts Page
       5. Navigating to List Posts Page
       6. Editing a Post
       7. Deleting a Post
       8. Creating a New Post
       9. Conclusion

    8. Interact with JavaScript

       1. Sending Data to JavaScript
       2. Subscriptions
       3. Receiving Data from JavaScript
       4. Protecting Boundaries between Elm and JavaScript
       5. Saving App State in Local Storage
       6. Retrieving App State from Local Storage
       7. Interacting with Web Components
       8. Conclusion
       9. Where To Go From Here?

2.  [25 Elm Examples](https://github.com/bryanjenningz/25-elm-examples)

    1. hello world 01
    2. hello world 02
    3. hello world 03
    4. hello world 04
    5. counter 05
    6. counter 06
    7. counter 07
    8. counter 08
    9. counter 09
    10. counter 10
    11. counter 11
    12. counter 12
    13. input box 13
    14. to-dos 14
    15. to-dos 15
    16. to-dos 16
    17. to-dos 17
    18. editable to-dos 18
    19. editable to-dos 19
    20. editable to-dos 20
    21. local storage editable to-dos 21
    22. local storage editable to-dos 22
    23. filter to-dos 23
    24. filter to-dos 24
    25. navigation to-dos 25

# 1. [Elm Programming](https://elmprogramming.com)

## 1. Intro

Hello there.

### 1. Why Elm?

Usable, faster than others. Maintainable, easy to add new features.

### 2. Feedback

Not much.

### 3. Who This Book is For

Read this book in sequential order.
Read and practice! You won't get
This tutorial's repo: https://github.com/pawanpoudel/beginning-elm-code

### 4. Conventions Used in This Book

meh.

### 5. Acknowledgement

meh.

### 6. About the Author

meh.

## 2. Getting Started

we will build a simple web page first.

### 1. Installation

1. install node.js: https://nodejs.org/en/download/
   `node --version` to make sure it's successful and ^7.
2. install elm repl: https://elm-lang.org/news/repl
3. install elm: https://guide.elm-lang.org/install/elm.html
   `elm --version` to make sure it's successful and ^0.19.
4. install vscode and its elm tools, setup etc.: https://github.com/elm-tooling/vscode-elm
5. install elm-format, to make it use standard style if you want to share it to the community.
   `npm install elm-format -g` to install.
   To use, example, `elm-format Main.elm`.
   Or, to use in vscode, https://github.com/avh4/elm-format#visual-studio-code-installation
6. install elm live for live reloading.
   `npm install --global elm elm-live`
   You can run it, for example, `elm-live Clock.elm --open`

### 2. Building a Simple Web Page

Okay, now let's create a web page, without elm.
See _2.2_homepage.html_

```html
<!DOCTYPE html>
<html>
  <head>
    <link
      rel="stylesheet"
      href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css"
    />

    <style>
      .jumbotron {
        background-color: #e6ffe6;
        text-align: center;
      }
    </style>
  </head>

  <body>
    <div class="jumbotron">
      <h1>Welcome to Dunder Mifflin!</h1>
      <p>
        Dunder Mifflin Inc. (stock symbol <strong>DMI</strong>) is a micro-cap
        regional paper and office supply distributor with an emphasis on
        servicing small-business clients.
      </p>
    </div>
  </body>
</html>
```

It's using Bootstrap CSS CDN, and also has some inline style. Now if you open the html file, it already looks nice.

Let's create it with elm. Make a new directory called _elmproject_ and open it with vscode. In terminal,
`elm init`
_y_
It will create the `elm.json` and `src`.

`elm.json` - Elm uses this file to determine which packages our project depends on. More on this later.

`src` - This directory is where all of our Elm files will be stored.
Create a new file called `Homepage.elm` inside the `src` directory and add the following code to it.

```elm
module Homepage exposing (main)

import Html exposing (..)
import Html.Attributes exposing (..)


view model =
    div [ class "jumbotron" ]
        [ h1 [] [ text "Welcome to Dunder Mifflin!" ]
        , p []
            [ text "Dunder Mifflin Inc. (stock symbol "
            , strong [] [ text "DMI" ]
            , text <|
                """
                ) is a micro-cap regional paper and office
                supply distributor with an emphasis on servicing
                small-business clients.
                """
            ]
        ]


main =
    view "dummy model"
```

Don’t worry about understanding the code above for now.
To run, `elm make src/Homepage.elm --output elm.js`
Note in mind, new version of elm needs same name for file and the module.
Now the `elm.js` should be created by the command. Create an html file in the root called `index.html`, with codes below.
Notice that we put our code inside html with `var app = Elm.Homepage.init`.
So, please make sure our name of main elm file(Homepage.elm), the `module Homepage exposing (main)` inside it, and the name inside the html file is the same.

```html
<!DOCTYPE html>
<script>
  <head>
    <link
      rel="stylesheet"
      href="https://maxcdn.bootstrapcdn.com/bootstrap/3.3.7/css/bootstrap.min.css"
    />

    <style>
      .jumbotron {
        background-color: #e6ffe6;
        text-align: center;
      }
    </style>
  </head>

  <body>
    <div id="elm-app-is-loaded-here"></div>

    <script src="elm.js"></script>
    <script>
      var app = Elm.Homepage.init({
        node: document.getElementById("elm-app-is-loaded-here")
      });
    </script>
  </body>
</script>
```

THe head is the same as before, with the CSS etc. In body, we created a div and gave it an id. We then loaded the elm.js file that was generated by previous command. That command compiles our Elm code and puts it in the elm.js file. Finally, we used the Elm.HomePage.init function to load our Elm app inside the elm-app-is-loaded-here div. Now you can open the `index.html` file.

### 3. Elm Platform

nah.

### 4. Elm Programming Language

nah.

### 5. Elm Compiler

![alt text](https://github.com/tengkusyafiq/elm-me-gusta/blob/master/elmprogramming/elm-compiler.svg)

Elm takes in multiple .elm files in our project and compiles them to a single .js file. So why do we have multiple .js files in the final build?

The reason behind it is that the code for our application doesn’t need to be written 100% in Elm. Once you realize what a delightful language Elm is, you will be hard-pressed to write your code in anything else. But even then you can write only a portion of your application in Elm if you choose to do so.

If you want to use Elm in js project little by little, see https://elm-lang.org/news/how-to-use-elm-at-work.

### 6. Elm Architecture

Elm Architecture is a set of patterns and language features for managing the flow of data in a program.
If you are coming to Elm from other languages such as JavaScript Ruby, or Python, you will notice that there is no separate framework for building applications in Elm. That’s because the Elm Architecture is baked into the language.

### 7. Elm Runtime

The Elm runtime is a system designed to support the execution of programs written in the Elm programming language.

### 8. elm make

We asked elm make to compile the code in our Elm file to JavaScript. If you look inside the elm.js file, you will realize that it contains thousands of lines of JavaScript code. But, wait a second — we didn’t write a ton of Elm code when we built our simple home page. It was barely fifteen lines of code.

In terminal we use `elm make src/Homepage.elm --output elm.js` before.
THen we import the output in index.html like below.

```html
<!DOCTYPE html>
<html>
  <head>
    ...
  </head>

  <body>
    . .
    <script src="elm.js"></script>
    . .
  </body>
</html>
```

We have to go through this process of creating a separate index.html file if we want to add any JavaScript code of our own or import a CSS file or use a Web Component in our app. But if we don’t want any of that, we can simply remove the --output flag. elm make will then automatically create an index.html file for us and put the compiled code in it. We don’t have to manually create that file like we did before. Go ahead and delete the beginning-elm/index.html file and run the following command from the beginning-elm directory in terminal.
`elm make src/Homepage.elm`
But it's best to stick with making our own html for best practice.

### 9. elm install

To install package. If we look at our elm project folder, we have `elm.json`, which looks like React's `package.json`. This is where it keeps all of the package details installed for the project.
Our project uses packages listed in `direct`. Some of those direct packages depend on other packages which are listed in `indirect`.
`elm make` looks inside the elm.json file and automatically installs all packages listed as dependencies. Once the initial project is setup, we shouldn’t modify elm.json by hand. Instead, we should use the `elm install` command to download packages from the online catalog.

For example, we need `elm/http`(making multiple HTTP requests to a server to retrieve data) package soon so let's install it.
`elm install elm/http`
It will install and update `elm.json` for you.

### 10. elm reactor

Elm provides an interactive development tool called elm reactor that lets us see the result of our code instantly.
Run `elm reactor` on the root project, open the localhost stated, navigate to the elm we are currently working on, `Homepage.elm` and you will see the web app WITHOUT CSS styling.
As of this writing, elm reactor doesn’t support loading external CSS frameworks such as Bootstrap. It has other limitations too. For example, it lacks live reloading — a technique that reloads a page automatically when the underlying code changes — thus requiring us to refresh the page manually every time we make a small change to our code to see the result. We will take a look at `elm-live` soon for better productivity.

### 11. elm repl

`elm repl` is a tool that lets us experiment with Elm. We will be using this tool extensively in the next chapter to learn the syntax and semantics of the Elm programming language. It's like running elm lines in command line, for learning etc., like you do when running python line directly in python command line.
run `elm repl` and you can type such as math stuff eg:`42/7.5`,`pi`, and other expressions eg: `List.reverse [ "Next", "Stop", "Pottersville" ]`

### 12. Ellie

Ellie also is good for learning if you want to code elm file online, like we did for our web app before offline.
Go to https://ellie-app.com/new, paste `Homepage.elm` into elm section and `index.html` into html section.
Ellie is good for trying a one-off experimental code. In addition to running simple programs, Ellie allows us to add Elm packages, work through compiler errors, and share our code with others. As of this writing, Ellie doesn’t provide a robust environment required for professional web application development. Hopefully, someday it will.

### 13. Conclusion

bye.

## 3. Elm Language Basics

Use elm repl to run simple elm code.

### 1. Simple Arithmetic

Example:
`1+2`
`12-1`
`41/10`
`9*2`
`42 * (200 - 8000)`

`/` will give you the exact, `//` will give you the integer only like below.

```elm
> 5 / 2
2.5 : Float

> 5 // 2
2 : Int
```

We can also write them in prefix style like below.

```elm
> (+) 1 2
3

> (-) 4534 789
3745
```

For power:

```elm
> 2 ^ 3 ^ 2
512

> (2 ^ 3) ^ 2
64
```

See more operators: https://elmprogramming.com/simple-arithmetic.html

### 2. Boolean

1. || - Boolean or - returns true if at least one input is True.
2. && - Boolean and - returns true only if both options are True.
3. not - Boolean negation - returns the opposite value of the input.
4. xor - Boolean exclusive-or - returns True if exactly one input is True.

```elm
> True || False
True

> False || False
False

> True && False
False

> True && True
True

> not True
False

> xor True False
True

> xor True True
False

> xor False False
False
```

In elm lamnugage, `null` or `0` is not `False`, so you can't use them as such.

### 3. Comparison

1.  == Equal
2.  /= Not Equal
3.  >     Greater than
4.  < Less than
5.  > = Greater than or equal to
6.  <= Less than or equal to
7.  max Find the larger of two
8.  min Find the smaller of two

Example:

```elm
> (5 == 5)
True

> 1 /= 2
True

> 10 < 7
False

> 100 > 99
True

> 7 >= 10
False

> 9 <= 9
True

> max 5 6
6

> min 3 8
3
```

### 4. Comments

#### Single line

```elm
42 + 1 -- This is a single line comment and will be ignored by Elm.
```

#### Multi-line

```elm
{-| Negate a boolean value.

    not True == False
    not False == True
-}
not : Bool -> Bool
not =
    Elm.Kernel.Basics.not
```

### 5. Expression

`3` is a number.
`x` is a symbol.
`-` is an operator.
`3x-5` is an expression.
`3x-5=7` is an equation (expression = expression).

### 6. Value

`3` is a number.
`1.5` is a float.
`c` is a character.
`pretzels` is a string.
`[ 1, 2, 3 ]` is a list.
`{ a = 1, b = 2 }` is a record
`( "first", "second" )` is a tuple
`someFunction x = x + 1` is a function

### 7. Constant

`x = (7 + 5) / 3` In this scenario, x can have only one value and that is 4. It can never change. It will remain 4 forever, until the end of time.

Other thing, name your constant with camel case, eg: `firstName`

### 8. If Expression

In elm, you must cover ALL of the possible way of outcomes, so is there is no `else`, it will throw an error.

```elm
> if velocity > 11.186 then "Godspeed" else "Come back"
"Godspeed"
```

You also can do equation like below.

```elm
> whatToDo = if velocity > 11.186 then "Godspeed" else "Come back"
"Godspeed"

> whatToDo
"Godspeed"
```

If you want to make a nested if, it is easier to write it in multi-line instead of one.

```elm
> velocity = 11
11

> speed = 7.67
7.67

> if velocity > 11.186 then \
|     "Godspeed" \
|   else if speed == 7.67 then \
|     "Stay in orbit" \
|   else \
|     "Come back"
"Stay in orbit"
```

Note that you don't need to type >, | and \ in command line.
We don’t need to add \ to the end of each line when we create a multi-line string in a file though.

### 9. Function

you can put the expression before into a function like below to use it multiple times.

```elm
> escapeEarth myVelocity = \
|   if myVelocity > 11.186 then \
|     "Godspeed" \
|   else \
|     "Come back"
<function>
```

Note that when writing the function body (if for example), you must use indentation.
`escapeEarth` is the function name.
`myVelocity` is the parameter.
Once we create a function, we need to apply it to a value to get a desired output.
Then you can use it like `escapeEarth 11.2` where `escapeEarth` is the function you want to use and `11.2` is the value of the parameter `myVelocity`.
Also, you can save the answer of it in new constant like below.
`whatToDo = escapeEarth 11.2`

> **Parameter vs Argument:**
> The terms parameter and argument are often used interchangeably although they are not the same. There is no harm in doing so, but just to clear things up, an argument is used to supply a value when applying the function (e.g. escapeEarth 11) whereas a parameter is used to hold onto that value in function definition (e.g. escapeEarth myVelocity).

#### Function with multiple parameters

THe function before only take one argument, right(we pass one number only)? Let's do it with multiple parameters so we can pass multiple arguments. Because we will write long codes, let's do it in our project instead of `elm repl`.
Use `ctrl + D` to exit `elm repl`.

> Please also name your file with camel case with uppercase first letter.

Let's make file `Playground.elm`, and use codes below.

```elm
module Playground exposing (main)
--make sure it has the same name as filename.

import Html
--import html module


escapeEarth myVelocity mySpeed =
    if myVelocity > 11.186 then
        "Godspeed"

    else if mySpeed == 7.67 then
        "Stay in orbit"

    else
        "Come back"


main =
    Html.text (escapeEarth 11.2 7.2)
```

In example above we set 2 parameters after the function name like `escapeEarth myVelocity mySpeed = <function body>`.
Then to pass the arguments, use `escapeEarth 11.2 7.2`.

The last function is main. The execution of all Elm applications start with this function. It’s a regular function like any other. It just happens to be the entry-point for an application. We apply a function called Html.text to the result produced by yet another function application: `escapeEarth 11.2 7.2`. Html.text takes a string and displays it on a browser.

To test it, run `elm reactor` like before and navigate to the elm file.

Oh, also, you can use a function in another function like `multiply a b = a * b` then pass the argument like `multiply 3 4`.

Let's try to apply it in our playground. Put codes below just above `main`.

```elm
computeSpeed distance time =
    distance / time


computeTime startTime endTime =
    endTime - startTime
```

Then use this `main` instead:

```elm
main =
    Html.text (escapeEarth 11 (computeSpeed 7.67 (computeTime 2 3)))
```

or a more readable one:

```elm
main =
    computeTime 2 3
        |> computeSpeed 7.67 --you can also pass only one argument even tho it has 2 parameters. Elm will see the argument passed as the first argument, and the second one will be taken next.
        |> escapeEarth 11
        |> Html.text
```

`|>`, or pipe operator (a.k.a. forward function application operator) made our code looks pretty. It pipes the result from previous expression to the next one. `computeSpeed 7.67` will take 1 from the previous result as the next argument. 7.67/1, this will equal to 7.67. It pass to `escapeEarth 11` as a second argument, so the result is "stay in orbit".

`<|` is the backward off pipe operator (a.k.a. backward function application operator). Just read it backward.

### 10. Let Expression

Often times, we want to define local constants and functions that we don’t want the rest of the code in our module to know about. We can define them inside a let expression. They won’t be visible outside the scope created by a let expression making them essentially private.
`let` is used with `in`.

```elm
escapeEarth myVelocity mySpeed fuelStatus =
    let
        escapeVelocityInKmPerSec =
            11.186

        orbitalSpeedInKmPerSec =
            7.67

        whereToLand fuel =
            if fuel == "low" then
                "Land on droneship"

            else
                "Land on launchpad"
    in
    if myVelocity > escapeVelocityInKmPerSec then
        "Godspeed"

    else if mySpeed == orbitalSpeedInKmPerSec then
        "Stay in orbit"

    else
        whereToLand fuelStatus

main =
    escapeEarth 10 6.7 "low"
        |> Html.text
```

No code outside escapeEarth function can access the `escapeVelocityInKmPerSec` and `orbitalSpeedInKmPerSec` constants. Yuo can also put function in let to use locally.

Please indent things inside `let`.
Save the file and refresh the url.

### 11. Case Expression

If you have so many conditions and want to match a pattern, better use `case`.
Let's see the different in using `if` and `case`.
Code below is using `if`.

```elm
weekday dayInNumber =
    if dayInNumber == 0 then
        "Sunday"

    else if dayInNumber == 1 then
        "Monday"

    else if dayInNumber == 2 then
        "Tuesday"

    else if dayInNumber == 3 then
        "Wednesday"

    else if dayInNumber == 4 then
        "Thursday"

    else if dayInNumber == 5 then
        "Friday"

    else if dayInNumber == 6 then
        "Saturday"

    else
        "Unknown day"

main =
    Html.text <| weekday 5
```

Code below is using `case`.

```elm
weekday dayInNumber =
    case dayInNumber of
        0 ->
            "Sunday"

        1 ->
            "Monday"

        2 ->
            "Tuesday"

        3 ->
            "Wednesday"

        4 ->
            "Thursday"

        5 ->
            "Friday"

        6 ->
            "Saturday"

        _ ->
            "Unknown day"

main =
    Html.text <| weekday 5
```

Notice that we're using `_` as `else`. Paste the code above in playgound, you should have "Friday".

You can also chain the case by adding code below, and edit the `main` as such.

```elm
hashtag dayInNumber =
    case weekday dayInNumber of --take weekday result as argument
        "Sunday" ->
            "#SinDay"

        "Monday" ->
            "#MondayBlues"

        "Tuesday" ->
            "#TakeMeBackTuesday"

        "Wednesday" ->
            "#HumpDay"

        "Thursday" ->
            "#ThrowbackThursday"

        "Friday" ->
            "#FlashbackFriday"

        "Saturday" ->
            "#Caturday"

        _ ->
            "#Whatever"
main =
    Html.text <| hashtag 5
```

By passing `5` to `hashtag`, but `hashtag` will look in `weekday` first. Then the result would be new argument to look into the `hashtag` case. So the result flow will be this way, `5` > `Friday` > `#FlashbackFriday`.

### 12. Indentation

`import` lines are optional. If they’re included, they’re listed right below the module definition. Both module and import lines must start at the left most column. The top-level function definitions are placed below the import lines. They too must start at the left most column.

However, the module and import lines are separated with only one blank line. These spacing rules are enforced by elm-format.

An if expression must be placed inside a function definition, otherwise Elm will throw an error.

Indented with four spaces.

The code inside the let area must be indented with at least one space, whereas the code inside the in area doesn’t need any indentation.

### 13. String

One line string: `"Pretzels"`
Multi-line string:

```elm
revelation =
    """
    It became very clear to me sitting out there today
    that every decision I've made in my entire life has
    been wrong. My life is the complete "opposite" of
    everything I want it to be. Every instinct I have,
    in every aspect of life, be it something to wear,
    something to eat - it's all been wrong.
    """
```

Try code above in playground with `main` below.

```elm
main =
    Html.text revelation
```

To escape "" or '', use backslash like `\"` or `\'`:

```elm
> "Michael Scott's Rabies Awareness \"Fun Run\" Race for the Cure"
"Michael Scott's Rabies Awareness \"Fun Run\" Race for the Cure"

> '\''
'\''
```

To escape the backslash itself, use itself lol:

```elm
> '\\'
'\\'
```

To calculate length of a string:

```elm
> String.length "Creed Bratton"
13
```

Optionally, you can import the String library.
`import String exposing (length)`
This way, we can just use `length` instead of `String.length`. But let's just stick to `String.length` because there is a `length` too in `List.length` module.

To check emptiness of a string:

```elm
 > String.isEmpty ""
True

> String.isEmpty "Kevin Malone"
False

> String.length "Kevin Malone" == 0
False
```

To combine strings, use `++`.

```elm
> "These pretzels are " ++ "makin' me thirsty!"
"These pretzels are makin' me thirsty!"
```

To combine characters, convert to string first.

```elm
> (String.fromChar 'p') ++ (String.fromChar 'r')
"pr"
```

You can also use `append`, `concat`, `join` to combine strings.

To split a string, use `split`, which is the opposite of `join`:

```elm
> String.split " " "Bears. Beats. Battlestar Gallactica."
["Bears.","Beats.","Battlestar","Gallactica."]
```

Code above will split every space character found.

To filter a string:
Let say, some user fill in the IC number in the database with dash(-) character, makes our database cannot read the numbers. So we need to filter out every dash character when reading the IC number database. We can use `String.filter` but we can't use right away. We need to use it like below.

```elm
> String.filter (\char -> char /= '-') "222-11-5555"
"222115555"
```

Changing case of a string:

```elm
> String.toUpper "I declare bankruptcy!"
"I DECLARE BANKRUPTCY!"

> String.toLower "Shhh. Be quiet."
"shhh. be quiet."
```

To trim unnecessary whitespaces:

```elm
> String.trim "    A band of backwoods mail-hating survivalists   \n"
"A band of backwoods mail-hating survivalists"
```

To find somethiung in string:

```elm
> String.contains "belie" "It’s not a lie if you believe it."
True
```

Note that it is case sensitive.

Extracting substring:

```elm
> String.slice 0 5 "Bears. Beets. Battlestar Galactica."
"Bears"

> String.slice -21 -1 "Bears. Beets. Battlestar Galactica."
"Battlestar Galactica" : String
```

### 14. Regular Expression

### 15. List

### 16. Array

### 17. Tuple

### 18. Record

### 19. Conclusion

## 4. Benefits of Using Elm

### 1. Immutability

### 2. Pure Functions

### 3. Solving Complex Problems with Simple Functions

### 4. Easy to Test

### 5. Type System

### 6. Easier Code Organization

### 7. Fuzz Testing

### 8. Pattern Matching

### 9. Conclusion

### 10. Architecture

### 11. Understand how the Elm Architecture helps us build robust front-end web applications

## 5. Elm Architecture

### 1. Model View Update - Part 1

### 2. Virtual DOM

### 3. Model View Update - Part 2

### 4. Side Effects

### 5. Commands

### 6. Conclusion

## 6. HTTP Requests

### 1. Fetching Data Using GET

### 2. Decoding JSON - Part 1

### 3. Decoding JSON - Part 2

### 4. RemoteData

### 5. Retrieving Data on Initialization

### 6. Conclusion

## 7. Single-Page Apps

### 1. What is a Single-Page App?

### 2. Restructuring Code

### 3. Creating Post Module

### 4. Creating List Posts Page

### 5. Navigating to List Posts Page

### 6. Editing a Post

### 7. Deleting a Post

### 8. Creating a New Post

### 9. Conclusion

## 8. Interact with JavaScript

### 1. Sending Data to JavaScript

### 2. Subscriptions

### 3. Receiving Data from JavaScript

### 4. Protecting Boundaries between Elm and JavaScript

### 5. Saving App State in Local Storage

### 6. Retrieving App State from Local Storage

### 7. Interacting with Web Components

### 8. Conclusion

### 9. Where To Go From Here?

# 2. [25 Elm Examples](https://github.com/bryanjenningz/25-elm-examples)

[x] download the repo.
[x] go through it one by one, test it yourself and make note.

## 1. hello world 01

``elm
-- This is how you write single-line comments in Elm.
{-
This is how you
write multi-line comments
in Elm.
-}
-- This is how you declare what your module name is and what values it exports.
-- We've chosen to name our module Main and we are exporting the value main that
-- we have defined below.

module Main exposing (main)

-- We're importing the Html module the text value available in our file, so we
-- can just reference it if we want.

import Html exposing (text)

-- The main value manages what gets displayed on the page. If we set the main
-- value to (text "Hello, World!"), then a text node with the string "Hello, World!"
-- will display on the page.

main =
text "Hello, World!"

````

```html
<html>
<head>
  <style>
    /* you can style your program here */
  </style>
</head>
<body>
  <main></main>
  <script>
    var app = Elm.Main.init({ node: document.querySelector('main') })
    // you can use ports and stuff here
  </script>
</body>
</html>
````

## 2. hello world 02

## 3. hello world 03

## 4. hello world 04

## 5. counter 05

## 6. counter 06

## 7. counter 07

## 8. counter 08

## 9. counter 09

## 10. counter 10

## 11. counter 11

## 12. counter 12

## 13. input box 13

## 14. to-dos 14

## 15. to-dos 15

## 16. to-dos 16

## 17. to-dos 17

## 18. editable to-dos 18

## 19. editable to-dos 19

## 20. editable to-dos 20

## 21. local storage editable to-dos 21

## 22. local storage editable to-dos 22

## 23. filter to-dos 23

## 24. filter to-dos 24

## 25. navigation to-dos 25

# Troubleshoots

## 1. Upgrading project from 0.19.0 to 0.19.1

https://github.com/elm/compiler/blob/master/docs/upgrade-instructions/0.19.1.md
You just change the version in elm.json to 0.19.1. That's all.

In this new version also, you need to name the file name as the same as the module name.

```

```

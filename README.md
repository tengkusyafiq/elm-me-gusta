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

### 6. Elm Architecture

### 7. Elm Runtime

### 8. elm make

### 9. elm install

### 10. elm reactor

### 11. elm repl

### 12. Ellie

### 13. Conclusion

## 3. Elm Language Basics

### 1. Simple Arithmetic

### 2. Boolean

### 3. Comparison

### 4. Comments

### 5. Expression

### 6. Value

### 7. Constant

### 8. If Expression

### 9. Function

### 10. Let Expression

### 11. Case Expression

### 12. Indentation

### 13. String

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

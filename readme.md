# Elm UI Explorer


![logo](https://raw.githubusercontent.com/kalutheo/elm-ui-explorer/master/explorer-logo-small.png)

[![Build Status](https://travis-ci.org/kalutheo/elm-ui-explorer.svg?branch=master)](https://travis-ci.org/kalutheo/elm-ui-explorer)

[UI Component Explorers](https://blog.hichroma.com/the-crucial-tool-for-modern-frontend-engineers-fb849b06187a) and [Style Guides](http://styleguides.io/) have been around for a while now.
We don't build pages anymore but components that are assembled together to build systems.

In the Elm world, components are just called views, and are defined as [pure functions](https://en.wikipedia.org/wiki/Pure_function).
Elm UI Explorer takes advantage of the composability and the purity of Elm and offers a way to showcase
your views and their states in a single tool.
This project is inspired by [React Storybook](https://storybook.js.org/) and styled with [Tailwind](https://tailwindcss.com/)


### How to use it ?

Here is a basic example of a button showcased in Elm UI Explorer:


Add this to your `Main.elm` file.

```elm
import Html
import Html.Attributes exposing (style)
import UIExplorer exposing (UIExplorerProgram, defaultConfig, explore, storiesOf)


button : String -> String -> Html.Html msg
button label bgColor =
    Html.button
        [ style "background-color" bgColor ]
        [ Html.text label ]


main : UIExplorerProgram {} () {}
main =
    explore
        defaultConfig
        [ storiesOf
            "Button"
            [ ( "SignIn", \_ -> button "Sign In" "pink", {} )
            , ( "SignOut", \_ -> button "Sign Out" "cyan", {} )
            , ( "Loading", \_ -> button "Loading please wait..." "white", {} )
            ]
        ]
```

Then in your Html add a link to the Elm UI Explorer stylesheet

```html
<link rel="stylesheet" type="text/css" href="https://cdn.jsdelivr.net/gh/kalutheo/elm-ui-explorer@master/assets/styles.css">
```

You can now run the `Main.elm` application with the tool of your choice.


[Checkout more examples here](https://github.com/kalutheo/elm-ui-explorer/tree/master/examples)
- Button Example [source](https://github.com/kalutheo/elm-ui-explorer/tree/master/examples/button)| [explorer demo](https://kalutheo.github.io/elm-ui-explorer/examples/button/explorer/index.html) |
[explorer with notes demo](https://kalutheo.github.io/elm-ui-explorer/examples/button/explorer-with-notes/index.html) | [app demo](https://kalutheo.github.io/elm-ui-explorer/examples/button/index.html)

- Design system [source](https://github.com/kalutheo/elm-ui-explorer/tree/master/examples/dsm/) | [explorer demo](https://kalutheo.github.io/elm-ui-explorer/examples/dsm/index.html)

### Main Features

- **Deep linking :** You can easily share UI Explorer states by copying and pasting the url ( ex:  attach them to your JIRA tickets, Pull Request etc... )

- **Categories :** Your UI Explorer can be divided into categories. Convenient if you have many views and you want to group them by family.


- **Plugins :** Elm UI Explorer has a mechanism that let you extend the tool by creating your own plugins. By defaults the library comes with [built in plugins](https://github.com/kalutheo/elm-ui-explorer/tree/master/src/UIExplorer/Plugins).


- **Customization :** You can make the header match your brand identity by changing colors, title and icons.




### Best Practices

- For hot reloading, it's recommended to use [Create Elm App](https://github.com/halfzebra/create-elm-app). [Elm Live](https://github.com/wking-io/elm-live) is also a great alternative that provides live reloading.

- In order to avoid CSS conflicts with built in UI Explorer Styles, consider using  [elm-css](https://package.elm-lang.org/packages/rtfeldman/elm-css/latest/) or [elm-ui](https://package.elm-lang.org/packages/mdgriffith/elm-ui/latest/). Theses tools use technics that prevent styles collisions by scoping the css.  

- Try to adopt [SDD (StoryBook Driven Development)](https://medium.com/nulogy/storybook-driven-development-a3c517276c07), creating UI this way can be very efficient.

- Use [Atomic Design](http://bradfrost.com/blog/post/atomic-web-design/) paradigm. This will help you build a scalable Design System.


- All ids (Story names and categories) should be unique (ex:  DropDown Menu, Loading, Loaded etc... )

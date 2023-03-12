# Summary:
- Controllers come from the MVC architecture.
- Elm Architecture is cooked into BubbleTea, therefore it would be awkward and a nightmare to maintain if I try to jam MVC architecture into this one.
---
# Related Stuff:
[[Spotify TUI]]
---
# Notes:
- I'm not sure MVC fits into Bubble tea, given a controller listens to updates, mutates data of either model, and controls the display by picking the appropriate view.
- Views are kind of an automatic thing, by that I mean we implement `tea.Model` by writing the implementation of the `tea.Model.View` function and it will get invoked by the framework.
- What I'm getting at is that if I were to create a `ControllerModel`, it would have its own view too, instead of me picking the view.
- The `Update` function for `ControllerModel` would also be a bit weird...
- It think MVC architecture is out of the question, given the philosophy of BubbleTea has the ELM architecture cooked into it:
  [Elm Architecture](https://guide.elm-lang.org/architecture/)
- In other words, it's like I'm trying to fit an architecture to work with another architecture, and that conflict is going to bite me in the butt.
- Therefore, I shouldn't think of MVC at all and get used to the Elm architecture.
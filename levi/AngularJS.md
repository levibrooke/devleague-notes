Topic: AngularJS
Date: 2/14/18
***

slides: http://devleague.slides.com/devleague/interactive-intro-angularjs

__Teaching version 1.6, referred to as AngularJS.__

## What is AngularJS
- Framework for dynamic web apps (single page apps)
- Allows templating in the browser instead of at the server level.

## MVC (model, view, controller)
- Model -> data
- Controller -> endpoint
- View -> client
- AngularJS is a MVC that sits at the view level.

## Models
- A Model is a singleton (only one in existence) defined by service.

## Templating (View)
- Using HTML for templating.
- Similar syntax to handlebars.

## Controller
- Layer between model and view.
- This layer should be as thin as possible (i.e. not doing any business logic).

## Two Way Data Binding
- Binds data between the controller and view using `$scope`

## Providers
- Value, constant, factory, service, provider
- May only use service mostly

## Directives
- Special markers on a DOM element that signals AngularJS's html compiler to attach a behavior or transform.
- Attribute, element, commennt, class

## Animations
- Animate w/ CSS instead of AngularJS

## Modules
- Containers for different parts of your app.
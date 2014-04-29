Cosmo.js(_BETA_)
======

Simpler Single Page Application MVC Framework

## Why?
I've used Backbone.js for a while now but after hacking on the new atom editor and using github's [SpacePen](http://github.com/atom/space-pen), I've realized that I can write client side apps with a different paradigm. SpacePen removes the need for templates and makes it easier to write more straightforward and intuitive(in my opinion) view objects.

So the goal of Cosmo.js is to make writing client side apps easier. I don't want to reinvent the wheel but I'd like to make a wheel I want to keep using though. Cosmo will have features I've realized I like to use from different places.  

  * Models/Collections/REST persistence from Backbone.js(They got it right)
  * Regions from Marionette.js
  * Computed properties from Ember.js

Usage
=====

Right now, Cosmo depends on SpacePen, jQuery, and Backbone. Soon, the necessary Backbone features will be incorporated to remove that extra dependency.

``` html
<script type='text/javascript' src="js/coffee-script.js"></script>
<script type='text/javascript' src="js/jquery-2.0.3.js"></script>
<script type='text/javascript' src="js/backbone.js"></script>
<script type='text/coffeescript' src="js/cosmo.js"></script>
```

## Cosmo.Router
Every app should be an instance of `Cosmo.Router`

``` coffeescript
class App extends Cosmo.Router
  initialize: ->
    # do stuff

MyApp = new App()
# start routing and do initialization
MyApp.start()
```

## Getters and Setters
Storing and retrieving data on the Router object should be done with its getters and setters.

``` coffeescript
MyApp.set 'name', 'akonwi'
MyApp.get 'akonwi' # => 'akonwi'
```

## Routing(_BETA_)
For now, routes are defined as functions of the extending Router. In order to render views, routes must call `@render someView`

``` coffeescript
class App extends Cosmo.Router
  # `home` should be the default implemented route for now...
  home: ->
    # stuff then...
    @render new HomeView
```

## Navigation
Use Cosmo.Router::go

``` coffeescript
MyApp.go 'home'
# or with up to two params
MyApp.go 'about', 'akonwi', {param2: true}
```

Even after implementing URL routing, I'd still like to also navigate by passing in data objects kind of like in Rails

``` coffeescript
akonwi = {id: 7, name: 'Akonwi Ngoh', age: 21}
MyApp.go akonwi # => would go to /users/akonwi or whatever
```

## Rendering
By default, render will display the given view into the div with the id 'container' in the DOM. This can be changed by calling `addRegions()` or overriding `render` in the extending Router class.

``` coffeescript
# change container to div#main-content. Use jquery selectors
MyApp.addRegions container: '#main-content', menu: '#side-bar'
```

## Regions
The container is the main default region but you can have as many as you want. When accessing regions, they will return jQuery objects

``` coffeescript
MyApp.get('regions').container # => whatever the jQuery looks like
```

## Data Persistence
Models and Collections are just instances of Backbone.Model and Collection for now

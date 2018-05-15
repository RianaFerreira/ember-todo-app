MVC framework

## Requirements
*   Node.js
*   NPM
*   GIT
*   Chrome ember inspector add-on
*   Firebase database

Ember command line utility `$ npm install -g ember-cli@1.13`
Create a new app `$ ember new <app-name>`
Start the server `$ ember server`

## [Routing](docs/routing/overview)
*   Create routes and link to templates.
*   Links between routes.
*   Creating layouts.

## [Helpers](docs/templates/helpers)
* Use moment.js to format dates displayed within the application.

## [EmberFire]:(https://github.com/firebase/emberfire) library version 1.6.2 to connect app to Firebase
Lock the library to version 1.6.2 to ensure compatibility with ember-cli 1.13.15
`$ ember install emberfire@1.6.2`

## [Showdown]:(https://github.com/showdownjs/showdown)
Markdown editing in text fields rendered in client.
Style templates with [bootstrap]:(http://getbootstrap.com/)
Apply the [starter template]:(http://getbootstrap.com/docs/4.1/examples/starter-template/) to `app/templates/application.hbs`

## [Models](docs/models/overview)
* models and data
* JSON API
* Ember-Data library
* CRUD functionality
* Connecting and using a database

## [Components](docs/components/overview)
* fundamentals and properties
* component classes
* component templates
* style components with bootstrap `bower install bootstrap`

## Scaffolding
Auto generate all related files for:
* model `$ ember g model user`
* route `$ ember g route users`
* nested route `$ ember g route users/new`
* controller `$ ember g controller users`
* controller action `$ ember g controller users/new`
* component `$ ember g component my-cool-component`


## Ember TodoList App
### Setup
Install 3rd party libraries with bower: boostrap, moment.js, and showdown.
Install ember firebase and create new ember-1-13-todolist project on [Firebase]:(https://console.firebase.google.com/project/ember-1-13-todo-list/settings/general/)

Update config/environment.js with Firebase configuration retrieved from the Firebase project settings:
```
contentSecurityPolicy: { 'connect-src': "'self' https://auth.firebase.com wss://*.firebaseio.com" },
firebase: 'https://ember-1-13-todo-list.firebaseio.com/',
```

Disable live reload in `.ember-cli`
```
{
  "disableAnalytics": false,
  "liveReload": false
}
```

Add references to the 3rd party libraries install with bower
```
module.exports = function(defaults) {
  var app = new EmberApp(defaults, {
    // Add options here
  });

  app.import('bower_components/bootstrap/dist/css/bootstrap.css');
  app.import('bower_components/moment/min/moment.min.js');
  app.import('bower_components/showdown/dist/showdown.min.js');

  return app.toTree();
};
```
Apply bootstrap default template and styles to application layout template.
Create an index template where the todo list components will be loaded.

### App Architecture
NB: Scaffolding a route auto generates the related template.
```
$ ember g route todos
$ ember g route todos/new
$ ember g route todos/edit
$ ember g controller todos
$ ember g controller todos/new
$ ember g controller todos/edit
$ ember g model todo
```

`router.js` is the app entry point for requests.
Update the auto generated routes to make todos a resource and allow the resource id to be passed to the edit action.
```
Router.map(function() {
  this.resource('todos', function() {
    this.route('new');
    this.route('edit', { path: '/edit/:todo_id' });
  });
});
```

#### Create skeleton app and feature blade

---
./brjs serve
---

open dashboard

---
./brjs create-app brjs-todo
./brjs create-bladeset brjs-todo todo
./brjs create-blade brjs-todo todo todoinput
---

view blade in workbench

#### Run tests

---
./brjs test ../apps/brjs-todo/todo/blades/todoinput
---

#### Change the value of property

assert property is "Hello Glasgow JS!"

tests fail

fix tests

show in workbench

#### Add blade to app

remove `<p>...</p>` from index.html

add to App.js

---
"use strict";

var PresenterComponent = require('br/presenter/component/PresenterComponent');
var TodoInputModel = require('brjstodo/todo/todoinput/ExamplePresentationModel');

var App = function() {
  var todoInputBlade = new PresenterComponent("brjstodo.todo.todoinput.view-template", new TodoInputModel());
  document.body.appendChild(todoInputBlade.getElement());
};

module.exports = App;
---

#### Update blade

---
cp ../../1-update-input/* ../apps/brjs-todo/
---

open workbench

show new model and new view

open app

#### Add new Blade

---
cp -r ../../2-list-blade/* ../apps/brjs-todo/
---

open Blade's workbench


#### Add both blades to app

---
"use strict";

var PresenterComponent = require('br/presenter/component/PresenterComponent');
var TodoInputModel = require('brjstodo/todo/todoinput/ExamplePresentationModel');
var TodoItemsModel = require('brjstodo/todo/todoitems/TodoItemsViewModel');

var App = function() {
  var todoInputBlade = new PresenterComponent("brjstodo.todo.todoinput.view-template", new TodoInputModel());
  document.body.appendChild(todoInputBlade.getElement());
  
  var todoItemsBlade = new PresenterComponent("brjstodo.todo.todoitems.view-template", new TodoItemsModel()); 
  document.body.appendChild(todoItemsBlade.getElement());
};

module.exports = App;
---


#### Change todoinput to use event hub

##### Update blade model
---
TodoInputViewModel.prototype.keyPressed = function( data, event ) {
  if( event.keyCode === ENTER_KEY_CODE ) {
  	var todoItem = { title: this.todoText.value.getValue() }

  	var ServiceRegistry = require('br/ServiceRegistry');
  	var eventHub = ServiceRegistry.getService('br.event-hub');
  	eventHub.channel('todo-list').trigger( 'todo-added', todoItem );

    this.todoText.value.setValue( '' );
  }

  return true;
};
---

##### Use eventhub in workbench

---
	var ServiceRegistry = require('br/ServiceRegistry');
	var eventHub = ServiceRegistry.getService('br.event-hub');
	eventHub.channel( 'todo-list' ).on( 'todo-added', function(e) { console.log(e); } );
---

#### Demo working app with 2 blades
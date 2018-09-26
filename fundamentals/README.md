* [first component](#first-component)
* [first component with angular cli](#first-component-with-angular-cli)
* [data binding](#data-binding)

# first component
In our app folder, which was created for us using __ng new__ command, we can create a new component by adding a new folder to the *app* folder in *src* folder. Let's call this new folder *users*.

Inside of this folder we need to define our *users* component, and that can be done by creating a new file, which we can name __users.component.ts__ (the name is optional though but it needs to be a typescript file so that we can user the features neccessary for this task).

Inside of this file, we start by importing *Component* from the *@angular/core* module. This *Component* is a class decorator which we can use to add additional logic to our classes. It expects a configuration object as its single argument which defines behaviour for our class. We can specify multiple properties/options in this configuration object, but for now, let's just use 2 of them that are recognized by the Component decorator -- __selector__ and __templateUrl__. 

* __selector__ should be a unique identifier, a string, which we then can use as a custom html tag to load this component into our final html code that will be rendered by the browser.

* __templateUrl__ is a relative path to html file that represents this conponent. Let's call our *users.component.html* and place some stuff in it. 

```html
<p>this is our Users Component</p>
```

*users.component.ts*
```javascript
import { Component } from "@angular/core";

@Component({
    selector: 'app-users',
    templateUrl: './users.component.html'
})
export class ServerComponent {}
```

Now that we have defined our component, we can can start using it by reffering to it with ```<app-users>``` tag.
But for that to work, we first need to tell the *app* component about this *users* component that we have just created. 

We can do that inside of *app.component.ts* file where we first need to import our *users* component and then, in the *declarations* array inside of *ngModule* decorator which decorates the *AppModule* class, we need to include this imported class.

*app.component.ts*
```javascript
import { BrowserModule } from '@angular/platform-browser';
import { NgModule } from '@angular/core';

import { AppComponent } from './app.component';
import { UsersComponent } from './users/users.component';

@NgModule({
  declarations: [
    AppComponent,
    UsersComponent
  ],
  imports: [
    BrowserModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
```

And now, we can open the *app.component.html* file and place there this custom html tag ```<app-users></app-users>``` and if we now start the application. We should see the html that we have defined inside of *users.component.html* template to be rendered in the browser.

# first component with angular cli 

The code above showes us how we can define our components by hand, but there is an option in angular CLI which does that for us, creating the folder for our component, adding the *ts* file as well as the *html* file and some others which we may or may not use. It also registers this new component in the *app.component.ts* file so that we can start using this newly created component right away.

The command is ```ng generate component name-of-the-component``` (or a short version of this command which is ```ng g c name-of-the-component```)

# data binding

Data binding is the how exchange data between the component and the template associated with it. There are multiple ways of how to achive this.

* string interpolation
* property binding 
* event binding 
* two-way binding

## string interpolation

This type of data binding is used to send data from inside of the component to the template. Inside of the component we 
can define some varable or a method that outputs a string and then use this in the template using double curly brackets syntax ```{{ name-of-the-variable }}```. Note that 

*in component file*
```javascript
export class MyComponent {
    const name = "John"
};
```

*in template*

```html
<p>name: {{ name }}</p>
```

## property binding

Again, this type of data binding is used to send data from component to template and it is used when we need to set some atribute of html element dynamically based on the data defined in our component. For example, we can set *disabled* property of the button this way. To achive this we need to wrap the property name with brackets and assign the name of the variable or method to it, enclosed in double quotation marks.

*in component file*
```javascript
export class MyComponent {
    const buttonIsDisabled = true;
};
```

*in template*

```html
<button [diabled]="buttonIsDisabled">Click me!</button>
```

## even binding 

Unlike the previous two methods, this one is used to send data from template to component by using events. The syntax used here is similar to one used in case of property binding but we change the brackets for braces and wrap the name of the event , such as *click* or *input* or any other normal JavaScript event. 

*in component file*
```javascript
export class MyComponent {
    onButtonClicked() {
        console.log('button has been clicked');
    }
};
```

*in template*

```html
<button (click)="onButtonClicked()">Click me!</button>
```

Right now, we are not passing any data back to the template though. For that we can specify what data we want to send back and prepend that name with dolar sign.

*in component file*
```javascript
export class MyComponent {
    onInputChange(event) {
        console.log('value of the input field is: ' + event.target.value);
    }
};
```

*in template*

```html
<input type="text" (input)="onInputChange($event)" />
```

## two way data binding 

We can also set up a two way data binding which is used to send data between component and template in both directions.
Here, unlike in other cases, we need to import *FormModule* from *@angular/forms* inside of *app.module.ts* file and add it to the *imports* array.

Syntax in this case is a combination of curly braces and brackets.

*in component file*
```javascript
export class MyComponent {
    name = "";
};
```

*in template*

```html
<input [(ngModel)]="name" type="text" />
<p>{{ name }}</p>
```

Now we have established the two way databinding between variable called *name* and the input field and if we type some text into that field, the name is immediatelly updated. But that is of course not all to it, if we change the value of that *name* variable in some other way, the value of our input field is updated as well.
 





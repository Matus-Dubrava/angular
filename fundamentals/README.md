* [first component](#first-component)
* [first component, with CLI](#first-component,-with-CLI)

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

## first component, with CLI 

The code above showes us how we can define our components by hand, but there is an option in angular CLI which does that for us, creating the folder for our component, adding the *ts* file as well as the *html* file and some others which we may or may not use. It also registers this new component in the *app.component.ts* file so that we can start using this newly created component right away.

The command is ```ng generate component name-of-the-component``` (or a short version of this command which is ```ng g c name-of-the-component```)




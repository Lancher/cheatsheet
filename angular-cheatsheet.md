# Agular 2

#### Architecture
 - Module: 
 - Component: html/css metadata (at leat one root component)
 - Directives: *ngif ...
 - Service: reponsive for talk to the backend server
 - Routers: route the url paths

#### Structure
 - TypeScript => Javascript

#### Component
 - selector: replace the **<my-app></my-app>** content
 - template: render html contesnt
 - ``: means to have multiple lines of htmls
 - directives: replace **<another></another>** by another component

```
import { Component } from '@angular/core';
import { AnotherComponent } from './another.component'

@Component({
  selector: 'my-app',
  template: `<h1>Hello World</h1>`
            `<another></another>`,
  style: [`h1 {
  	color: red      	
  }`],
  directives: [AnotherComponent]
})

export class AppComponent {}
```
 

# Agular 2

[course](https://www.youtube.com/watch?v=zj7_4VDFQPA&list=PLC3y8-rFHvwg5gEu2KF4sbGvpUqMRSBSW)

### Architecture
 - __Module__: 
 - __Component__: html/css metadata (at leat one root component)
 - __Directives__: *ngif ...
 - __Service__: reponsive for talk to the backend server
 - __Routers__: route the url paths

### Structure
 - Compile TypeScript => Javascript

### Component
 - __selector__: replace the `<my-app></my-app>` content
 - __template__: render html contesnt
 - __``__: means to have multiple lines of htmls
 - __style__: css syntax which restrict to the component 
 - __directives__: replace `<another></another>` by another component

```angular
import { Component } from '@angular/core';
import { AnotherComponent } from './another.component'

@Component({
  selector: 'my-app',
  template: `<h1>Hello World</h1>
             <another></another>`,
  style: [`h1 {
  	color: red      	
  }`],
  directives: [AnotherComponent]
})

export class AppComponent {}
```
 
### Component Data Binding
 - __{{ }}__: bracket replacement
 - __[]=""__: attribute replacement

```angular
import { Component } from '@angular/core';
import { AnotherComponent } from './another.component'

@Component({
  selector: 'my-app',
  template: `<h1>{{ title }}</h1>`
            `<img [src]="imgLink">`,
})

export class AppComponent {
	public title = 'Hello World';
	public imgLink = 'http://comomd.tw/h,png'
}
```

### Component Style Binding
 - __[class.className]="true or false"__: whether to set the class
 - __[class.style]="applyBlue ? 'blue' : 'orange' "__: set class style

```angular
import { Component } from '@angular/core';
import { AnotherComponent } from './another.component'

@Component({
  selector: 'my-app',
  template: `<h1 [class.blueClass]="applyBlue">Hello World</h1>
             <div [style.color]="applyRed ? 'res' : 'orange' ">`,
  style: [`.blueClass {
  	color: blue
  }`],  
})

export class AppComponent {
	public applyBlue = true;
	public applyRed = true;
}
```

### ngModel
- __data binding__: once the variables change, the view also update
- __[(ngModel)]__: ??? + property binding

```angular
import { Component } from '@angular/core';
import { AnotherComponent } from './another.component'

@Component({
  selector: 'my-app',
  template: `<input type="text" [(ngModel)]="firstName">
             <input type="text" [(ngModel)]="lastName">
             Full Name: {{ firstName }} {{ lastName }}`,
  style: [`.blueClass {
  	color: blue
  }`],  
})

export class AppComponent {
	public firstName = true;
	public lastName = true;
}
```

### ngif/ngSwitch/ngFor
- __ngif__: whether to show the element
- __ngSwitch/ngSwitchWhen__: swtich control flow
- __ngFor__: for loop control flow


```angular
import { Component } from '@angular/core';
import { AnotherComponent } from './another.component'

@Component({
  selector: 'my-app',
  template: `<p *ngif="showElement">Yes, I am the element</p>
             <div [ngSwitch]="color">
               <p *ngSwitchWhen="'red'">Red One</p>
               <p *ngSwitchWhen="'blue'">Blue One</p>
               <p *ngSwitchWhen="'green'">Green One</p>
             </div>
             <ul>
               <li *ngFor="let color of colors">{{ color }}</li>
             </ul>`,
  style: [`.blueClass {
  	color: blue
  }`],  
})

export class AppComponent {
	public showElement = true;
	public color = "red";
	public colors = ["red", "blue", "green"];
}
```

### ngClass/ngStyle
- __ngClass__: bind css class to html elements
- __ngStyle__: bind css property to html elements

```angular
import { Component } from '@angular/core';
import { AnotherComponent } from './another.component'

@Component({
  selector: 'my-app',
  template: `<p [ngClass]="{classOne: one, classTwo: two}">Godjj</p>
             <button (click)="toggle()">Toggle</button>
             
             <p [ngStyle]="{'font-size': fontSize}"></p>`,
  style: [
    `.oneClass { color: blue}
     .twoClass { background-color: red}`
  ],  
})

export class AppComponent {
	public one = true;
	public two = true;
	toggle() {
		this.one = !this.one;
		this.two = !this.two;
	}
	
	public fontSize = '30px';
}
```

### parent >> child / child >> parent
- __input (parent >> child)__: 
	1. Set a variable as `input` in child compoment
	2. In parent component, we set `<input>` link to children `property binding`.
	
```angular
// Parent Component

import { Component } from '@angular/core';
import { AnotherComponent } from './another.component'
@Component({
  selector: 'my-app',
  template: `<input type="text" #ptext (keyup)="0">
             <another [parentData]="ptext.val"></another>`,
  directives: [AnotherComponent]
})
export class AppComponent {}


// Child Component
	
import { Component } from '@angular/core';
@Component({
  selector: 'my-app',
  template: `from parent: {{ parentData }}`,
  input: ['parentData'],
})
export class AnotherComponent {
  public parentData: string;
}
```

- __outout (chid >> parent)__: 
	1. Pass the EventEmitter to parent component
	2. In parent component, we set event handler

```angular
// Parent Component

import { Component } from '@angular/core';
import { AnotherComponent } from './another.component'
@Component({
  selector: 'my-app',
  template: `<another (childEvent)="childData=$event"></another>
             {{ childData }}`,
  directives: [AnotherComponent]
})
export class AppComponent {
  public childData: string;
}


// Child Component
	
import { Component } from '@angular/core';
import { EventEmitter } from '@angular/core';
@Component({
  selector: 'my-app',
  template: `<input #childtext (keyup)="onChange(childtext.value)">`,
  output: ['childEvent'],
})
export class AnotherComponent {
  childEvent = new EventEmitter<string>();
  onChange(value:string) {
    this.childEvent.emit(value);
  }
}
```

### Pipe
- uppercase
- lowercase
- slice
- replace

```
import { Component } from '@angular/core';

@Component({
  selector: 'my-app',
  template: `{{ name | uppercase }}
             {{ name | lowercase }}
             {{ name | slice: '2':'4' }}`
             {{ name | replace: 'Hello': 'The' }}
             {{ 8.576 | number: '1.2-3' }}`,
  directives: [AnotherComponent]
})
export class AppComponent {
  name="Hello World";
}
```


























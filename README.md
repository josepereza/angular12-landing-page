# Angular Landing Page
 An Angular Material landing page

This project was generated with [Angular CLI](https://github.com/angular/angular-cli) version 12.0.4.
## Using MediaMatcher
https://www.digitalocean.com/community/tutorials/angular-breakpoints-angular-cdk
* MediaMatcher is a service that wraps around JavaScript’s matchMedia. As with BreakpointObserver.observe, it can also be used to observe changes in the viewport size against a given media query.

Here is an example that checks if min-width is 500px wide:
```
import { Component, OnInit, OnDestroy } from '@angular/core';
import { MediaMatcher } from '@angular/cdk/layout';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit, OnDestroy {
  matcher!: MediaQueryList;

  constructor(public mediaMatcher: MediaMatcher) {}

  ngOnInit() {
    this.matcher = this.mediaMatcher.matchMedia('(min-width: 500px)');

    this.matcher.addEventListener('change', this.myListener);
  }

  ngOnDestroy() {
    this.matcher.removeEventListener('change', this.myListener);
  }

  myListener(event: { matches: any; }) {
    console.log(event.matches ? 'match' : 'no match');
  }
}
```
## Development server

Run `ng serve` for a dev server. Navigate to `http://localhost:4200/`. The app will automatically reload if you change any of the source files.
# TUTORIAL
## How To Detect Breakpoints Using the Angular CDK
Angular
By Alligator.io

Last Validated onAugust 9, 2021 Originally Published onMarch 22, 2018 82.2kviews
Introduction
The Angular CDK has a layout package with services to detect viewport sizes and matches against media queries. This allows you full control over the UI and to adapt to different screen sizes.

In this article, you will apply the CDK’s layout module in Angular projects.

Prerequisites
If you would like to follow along with this article, you will need:

Node.js installed locally, which you can do by following How to Install Node.js and Create a Local Development Environment.
This tutorial will also assume you have @angular/cli installed globally.
Some familiarity with CSS media queries.
This tutorial was verified with Node v16.6.1, npm 7.20.3, @angular/core v12.2.0, and @angular/cdk v12.2.0.

### Setting Up the Project
You can use @angular/cli to create a new Angular Project.

In your terminal window, use the following command:

ng new AngularBreakpointsExample --style=css --routing=false --skip-tests
 
This will configure a new Angular project with styles set to “CSS” (as opposed to “Sass”, Less", or “Stylus”), no routing, and skipping tests.

Navigate to the newly created project directory:

cd AngularBreakpointsExample
 
Next, install @angular/cdk:

npm install @angular/cdk@12.2.0
 
Then import the layout module and and add it to your NgModule’s list of imports:
```
src/app/app.module.ts
import { NgModule } from '@angular/core';
import { BrowserModule } from '@angular/platform-browser';
import { LayoutModule } from '@angular/cdk/layout';

import { AppComponent } from './app.component';

@NgModule({
  declarations: [
    AppComponent
  ],
  imports: [
    BrowserModule,
    LayoutModule
  ],
  providers: [],
  bootstrap: [AppComponent]
})
export class AppModule { }
 ```
You can now start using the available services and utilities in your components. Let’s discuss each of them.

## Using BreakpointObserver.observe and BreakpointState
The observe method returns an observable of type BreakpointState and can be used to observe when the viewport changes between matching a media query or not.

Here’s an example where a message is logged to the console if the viewport size changes between being less than 500px and equal to or more than 500px:
```
src/app/app.component.ts
import { Component, OnInit } from '@angular/core';
import {
  BreakpointObserver,
  BreakpointState
} from '@angular/cdk/layout';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  constructor(public breakpointObserver: BreakpointObserver) {}

  ngOnInit() {
    this.breakpointObserver
      .observe(['(min-width: 500px)'])
      .subscribe((state: BreakpointState) => {
        if (state.matches) {
          console.log('Viewport width is 500px or greater!');
        } else {
          console.log('Viewport width is less than 500px!');
        }
      });
  }
}
 ```
Note: You may also need to remove {{ title }} from app.component.html to prevent an error.

The BreakpointState interface gives us a boolean property called matches.

## Using Breakpoints
Instead of using hand-written media queries, we can also make use of the Breakpoints object, which gives us keys for common breakpoints:
```
src/app/app.component.ts
import { Component, OnInit } from '@angular/core';
import {
  BreakpointObserver,
  Breakpoints,
  BreakpointState
} from '@angular/cdk/layout';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  constructor(public breakpointObserver: BreakpointObserver) {}

  ngOnInit() {
    this.breakpointObserver
      .observe([Breakpoints.Small, Breakpoints.HandsetPortrait])
      .subscribe((state: BreakpointState) => {
        if (state.matches) {
          console.log(
            'Matches small viewport or handset in portrait mode'
          );
        }
      });
  }
}
 ```
This example uses the predefined breakpoints for Breakpoints.Small and Breakpoints.HandsetPortrait.

## Using BreakpointObserver.isMatched
For one-off matching, we can use the isMatching method instead.
```
src/app/app.component.ts
import { Component, OnInit } from '@angular/core';
import {
  BreakpointObserver,
  BreakpointState
} from '@angular/cdk/layout';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit {
  constructor(public breakpointObserver: BreakpointObserver) {}

  ngOnInit() {
    if (this.breakpointObserver.isMatched('(min-height: 40rem)')) {
      console.log('Viewport has a minimum height of 40rem!');
    }
  }
}
 ```
This will log a message if the viewport is at least 40rem tall when the component initializes.

## Using MediaMatcher
MediaMatcher is a service that wraps around JavaScript’s matchMedia. As with BreakpointObserver.observe, it can also be used to observe changes in the viewport size against a given media query.

Here is an example that checks if min-width is 500px wide:
```
src/app/app.component.html
import { Component, OnInit, OnDestroy } from '@angular/core';
import { MediaMatcher } from '@angular/cdk/layout';

@Component({
  selector: 'app-root',
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css']
})
export class AppComponent implements OnInit, OnDestroy {
  matcher!: MediaQueryList;

  constructor(public mediaMatcher: MediaMatcher) {}

  ngOnInit() {
    this.matcher = this.mediaMatcher.matchMedia('(min-width: 500px)');

    this.matcher.addEventListener('change', this.myListener);
  }

  ngOnDestroy() {
    this.matcher.removeEventListener('change', this.myListener);
  }

  myListener(event: { matches: any; }) {
    console.log(event.matches ? 'match' : 'no match');
  }
}
 ```
The difference with BreakpointObserver.observe is that MediaMatcher gives us access to the native MatchQueryList object, which may be needed in certain scenarios.
## Code scaffolding

Run `ng generate component component-name` to generate a new component. You can also use `ng generate directive|pipe|service|class|guard|interface|enum|module`.

## Build

Run `ng build` to build the project. The build artifacts will be stored in the `dist/` directory.

## Running unit tests

Run `ng test` to execute the unit tests via [Karma](https://karma-runner.github.io).

## Running end-to-end tests

Run `ng e2e` to execute the end-to-end tests via a platform of your choice. To use this command, you need to first add a package that implements end-to-end testing capabilities.

## Further help

To get more help on the Angular CLI use `ng help` or go check out the [Angular CLI Overview and Command Reference](https://angular.io/cli) page.



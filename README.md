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



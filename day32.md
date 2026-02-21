## Day 32

I learned more about Angular 21, and how to set up the project.

First we need to install the Angular CLI

```
yarn global add @angular/cli
```

Then you can start a new project with

```
ng new <project-name>
```

I've learned about:

- Signals
- What's somehow different between 21 and older versions
- Created the first page

Also learned that we can generate components with:

```
ng g c <name of component>
```

This will generate files such as

- name.component.ts
- name.component.css
- name.spec.ts
- name.component.html

Then, we can include this in the `imports` of the `app` or in any component:

```
import { Component } from '@angular/core';
import { HeaderComponent } from './header/header.component';
import { UserComponent } from './user/user.component';

@Component({
  selector: 'app-root',
  standalone: true,
  imports: [HeaderComponent, UserComponent],
  templateUrl: './app.component.html',
  styleUrls: ['./app.component.css'],
})
export class AppComponent {
  title = 'angular-standalone-components';
}
```

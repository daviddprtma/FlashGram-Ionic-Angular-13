# FlashGram-Ionic-Angular-13
Flashgram merupakan sebuah apilkasi yang mirip Instagram dimana aplikasi ini dibuat untuk dapat berbagi cerita dan momen mereka bersama. FlashGram ini dibuat secara berkelompok oleh 3 orang yaitu Saya, Noor, dan Pandu. Semoga dengan hadirnya aplikasi ini, dapat membantu masyarakat untuk dapat mengkesperesikan momen mereka melalui aplikasi ini. 

[![Build Status](https://img.shields.io/endpoint.svg?url=https%3A%2F%2Factions-badge.atrox.dev%2Fionic-team%2Fionic-storage%2Fbadge%3Fref%3Dmain&style=flat)](https://actions-badge.atrox.dev/ionic-team/ionic-storage/goto?ref=main)

# Ionic Storage

A simple key-value Storage module for Ionic apps. This utility uses the best storage engine available on the platform without having to interact with it directly (some configuration required, see docs below).

As of 3.x, this library now supports any JavaScript project (old versions only supported Angular), and Angular-specific functionality has been moved to a new `@ionic/storage-angular` package.

Out of the box, Ionic Storage will use `IndexedDB` and `localstorage` where available. To use SQLite for native storage, see the [SQLite Installation](#sqlite-installation) instructions.

For teams building security sensitive applications requiring encryption, 3.x now supports encryption through Ionic Secure Storage, see [Encryption Support](#encryption-support) for instructions on using it.

## Installation

```shell
npm install @ionic/storage
```

If using Angular, install the `@ionic/storage-angular` library instead:

### With Angular

Usage in Angular using Services and Dependency Injection requires importing the `IonicStorageModule` and then injecting the `Storage` class.

First, edit your NgModule declaration in `src/app/app.module.ts` or in the module for the component you'll use the storage library in, and add  `IonicStorageModule` as an import:

```typescript
import { IonicStorageModule } from '@ionic/storage-angular';

@NgModule({
  imports: [
    IonicStorageModule.forRoot()
  ]
})
export class AppModule { }
```

Next, inject `Storage` into a component. Note: this approach is meant for usage in a single component (such as `AppComponent`). In this case, `create()` should only be called once. For use in multiple components, we recommend creating a service (see next example).

```typescript
import { Component } from '@angular/core';
import { Storage } from '@ionic/storage-angular';

@Component({
  selector: 'app-root',
  templateUrl: 'app.component.html'
})
export class AppComponent {

  constructor(private storage: Storage) {
  }

  async ngOnInit() {
    // If using a custom driver:
    // await this.storage.defineDriver(MyCustomDriver)
    await this.storage.create();
  }
}
```

For more sophisticated usage, an Angular Service should be created to manage all database operations in your app and constrain all configuration and database initialization to a single location. When doing this, don't forget to register this service in a `providers` array in your `NgModule` if not using `providedIn: 'root'`, and ensure that the `IonicStorageModule` has been initialized in that `NgModule` as shown above. Here's an example of what this service might look like:

```typescript
import { Injectable } from '@angular/core';

import { Storage } from '@ionic/storage-angular';

@Injectable({
  providedIn: 'root'
})
export class StorageService {
  private _storage: Storage | null = null;

  constructor(private storage: Storage) {
    this.init();
  }

  async init() {
    // If using, define drivers here: await this.storage.defineDriver(/*...*/);
    const storage = await this.storage.create();
    this._storage = storage;
  }

  // Create and expose methods that users of this service can
  // call, for example:
  public set(key: string, value: any) {
    this._storage?.set(key, value);
  }
}
```

Then, inject the `StorageService` into your pages and other components that need to interface with the Storage engine.

## Configuration

The Storage engine can be configured both with specific storage engine priorities, or custom configuration
options to pass to localForage. See the localForage config docs for possible options: https://github.com/localForage/localForage#configuration

### Angular configuration

```typescript
import { Drivers, Storage } from '@ionic/storage';
import { IonicStorageModule } from '@ionic/storage-angular';

@NgModule({
  //...
  imports: [
   IonicStorageModule.forRoot({
     name: '__mydb',
     driverOrder: [Drivers.IndexedDB, Drivers.LocalStorage]
   })
 ],
 //...
})
export class AppModule { }
```

<h1 align="center">Angular - The modern web developer's platform.</h1>

<p align="center">
  <img src="aio/src/assets/images/logos/angular/angular.png" alt="angular-logo" width="120px" height="120px"/>
  <br>
  <i>Angular is a development platform for building mobile and desktop web applications
    <br> using Typescript/JavaScript and other languages.</i>
  <br>
</p>

<p align="center">
  <a href="https://www.angular.io"><strong>www.angular.io</strong></a>
  <br>
</p>

<p align="center">
  <a href="CONTRIBUTING.md">Contributing Guidelines</a>
  ·
  <a href="https://github.com/angular/angular/issues">Submit an Issue</a>
  ·
  <a href="https://blog.angular.io/">Blog</a>
  <br>
  <br>
</p>

<p align="center">
  <a href="https://circleci.com/gh/angular/workflows/angular/tree/master">
    <img src="https://img.shields.io/circleci/build/github/angular/angular/master.svg?logo=circleci&logoColor=fff&label=CircleCI" alt="CI status" />
  </a>&nbsp;
  <a href="https://www.npmjs.com/@angular/core">
    <img src="https://img.shields.io/npm/v/@angular/core.svg?logo=npm&logoColor=fff&label=NPM+package&color=limegreen" alt="Angular on npm" />
  </a>&nbsp;
  <a href="https://discord.gg/angular">
    <img src="https://img.shields.io/discord/463752820026376202.svg?logo=discord&logoColor=fff&label=Discord&color=7389d8" alt="Discord conversation" />
  </a>
</p>

<hr>

## Documentation

Get started with Angular, learn the fundamentals and explore advanced topics on our documentation website.

- [Getting Started][quickstart]
- [Architecture][architecture]
- [Components and Templates][componentstemplates]
- [Forms][forms]
- [API][api]

### Advanced

- [Angular Elements][angularelements]
- [Server Side Rendering][ssr]
- [Schematics][schematics]
- [Lazy Loading][lazyloading]

## Development Setup

### Prerequisites

- Install [Node.js] which includes [Node Package Manager][npm]

### Setting Up a Project

Install the Angular CLI globally:

```
npm install -g @angular/cli
```

Create workspace:

```
ng new [PROJECT NAME]
```

Run the application:

```
cd [PROJECT NAME]
ng serve
```

Angular is cross-platform, fast, scalable, has incredible tooling, and is loved by millions.

## Quickstart

[Get started in 5 minutes][quickstart].

## Ecosystem

<p>
  <img src="/docs/images/angular-ecosystem-logos.png" alt="angular ecosystem logos" width="500px" height="auto">
</p>

- [Angular Command Line (CLI)][cli]
- [Angular Material][angularmaterial]

## Changelog

[Learn about the latest improvements][changelog].

## Upgrading

Check out our [upgrade guide](https://update.angular.io/) to find out the best way to upgrade your project.

## Contributing

### Contributing Guidelines

Read through our [contributing guidelines][contributing] to learn about our submission process, coding rules and more.

### Want to Help?

Want to report a bug, contribute some code, or improve documentation? Excellent! Read up on our guidelines for [contributing][contributing] and then check out one of our issues labeled as <kbd>[help wanted](https://github.com/angular/angular/labels/help%20wanted)</kbd> or <kbd>[good first issue](https://github.com/angular/angular/labels/good%20first%20issue)</kbd>.

### Code of Conduct

Help us keep Angular open and inclusive. Please read and follow our [Code of Conduct][codeofconduct].

## Community

Join the conversation and help the community.

- [Twitter][twitter]
- [Discord][discord]
- [Gitter][gitter]
- [YouTube][youtube]
- [StackOverflow][stackoverflow]
- Find a Local [Meetup][meetup]

[![Love Angular badge](https://img.shields.io/badge/angular-love-blue?logo=angular&angular=love)](https://www.github.com/angular/angular)

**Love Angular? Give our repo a star :star: :arrow_up:.**

[contributing]: CONTRIBUTING.md
[quickstart]: https://angular.io/start
[changelog]: CHANGELOG.md
[ng]: https://angular.io
[documentation]: https://angular.io/docs
[angularmaterial]: https://material.angular.io/
[cli]: https://cli.angular.io/
[architecture]: https://angular.io/guide/architecture
[componentstemplates]: https://angular.io/guide/displaying-data
[forms]: https://angular.io/guide/forms-overview
[api]: https://angular.io/api
[angularelements]: https://angular.io/guide/elements
[ssr]: https://angular.io/guide/universal
[schematics]: https://angular.io/guide/schematics
[lazyloading]: https://angular.io/guide/lazy-loading-ngmodules
[node.js]: https://nodejs.org/
[npm]: https://www.npmjs.com/get-npm
[codeofconduct]: CODE_OF_CONDUCT.md
[twitter]: https://www.twitter.com/angular
[discord]: https://discord.gg/angular
[gitter]: https://gitter.im/angular/angular
[stackoverflow]: https://stackoverflow.com/questions/tagged/angular
[youtube]: https://youtube.com/angular
[meetup]: https://www.meetup.com/find/?keywords=angular"


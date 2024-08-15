# How Content Ends up on the Screen? 🛠️
The `index.html` file in *src* folder is the root file for displaying data to the UI. Let's have a look at the file:

```html
    <!doctype html>
    <html lang="en">
    <head>
        <meta charset="utf-8">
        <title>FirstAngularApp</title>
        <base href="/">
        <meta name="viewport" content="width=device-width, initial-scale=1">
        <link rel="icon" type="image/x-icon" href="favicon.ico">
    </head>
    <body>
        <app-root></app-root>
    </body>
    </html>
```

From the code above, when we run the application we get the below UI:

//image0

Looking at the image above and the `index.html` code above. It is clearly visible that the UI has more that what is provided on the `index.html` code, but how is that possible. Below is the `index.html` *body* tag which is responsible for the outcome we see on the UI/browser:

```html
    <body>
        <app-root></app-root>
    </body>
```
If `<app-root></app-root>` is what we should be seeing on the UI/broswer then where do we get what we saw from the image above?

## main.ts 📂
It's the code in this folder that actually will be executed when your website loads up.

```ts
    import { bootstrapApplication } from '@angular/platform-browser';
    import { appConfig } from './app/app.config';
    import { AppComponent } from './app/app.component';

    bootstrapApplication(AppComponent, appConfig)
    .catch((err) => console.error(err));
```

But how is that possible since there are no imports/script tags on the `index.html` code base?

If you actually view the `Debug` content of the loaded browser page by pressing the shortcut `F12` or right-click on the page and select *inspect*, we see the below results:

//image1

We can see that indeed there are scripts injected to the `index.html` file. These scripts are inject on the file by `angular CLI` when you build your application (using `ng serve`).

Then:

```ts
    import { bootstrapApplication } from '@angular/platform-browser';
```
The code above executes a *function* called `bootstrapApplication` which is taken from the path `@angular/platform-browser` of the angular package. This *function* will look for the angular component. It then looks for the component in the `index.html` file and tries to replace the element tag of your *custom component* with the *markup* you defined for your *custom component*.

For our case it's the `AppComponent` which is imported from the path `./app/app.component` which gets passed to the bootstrap function:

```ts
    bootstrapApplication(AppComponent, appConfig)
```

Now if we follow the path `./app/app.component` we get:

```ts
    import { Component } from '@angular/core';
    import { RouterOutlet } from '@angular/router';

    @Component({
        selector: 'app-root',
        standalone: true,
        imports: [RouterOutlet],
        templateUrl: './app.component.html',
        styleUrl: './app.component.scss'
    })
    export class AppComponent {
        title = 'first-angular-app';
    }
```
From the above we are importing something called `AppComponent` and if we look at the above `app.component.ts` file code we see that we are exporting the `class AppComponent{}`

```ts
    export class AppComponent {
        title = 'first-angular-app';
    }
```

So this class in Angular creates a component which is anhtml element. It does that by using the below code:

```ts
    @Component({
    selector: 'app-root',
    standalone: true,
    imports: [RouterOutlet],
    templateUrl: './app.component.html',
    styleUrl: './app.component.scss'
    })
```

The above code is called a decorator. Now where does that decorator come from? If we look at the `app.component.ts` file:

```ts
    import { Component } from '@angular/core';
```

We see that the component directory path is `@angular/core`, which is where import the core package that is part of the framework.

The `selector` property inside the decorator tells angular which elements to look for in the html code so that those elements can be replaced by this component and it's markup. 

```ts
    selector: 'app-root'
```
The markup of that component will be stored in the `templateUrl` property value (path).

```ts
    templateUrl: './app.component.html'
```






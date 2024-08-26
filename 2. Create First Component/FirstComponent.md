# Components.
In **AngularJS**, a component is a special kind of directive that uses a simpler configuration which is suitable for a `component-based` application structure. Components are a key part of AngularJS 1.5 and later versions, and they help to create reusable, encapsulated pieces of UI with their own logic.

A component in AngularJS is defined using the `.component()` method, which is a higher-level abstraction of the `.directive()` method. Components are particularly useful for creating reusable and maintainable code.

## Key Features of AngularJS Components:
1. **Simplified Configuration**: Components have a simpler configuration compared to directives.
2. **Isolated Scope**: Components have an isolated scope by default.
3. **Controller**: Each component has its own controller.
4. **Template**: Components have their own template or templateUrl.
5. **Bindings**: Components can have input and output bindings.

## Adding a new component.
Since we have created our first application, we now going to add a new component. But let's first see the componennt that already exists withing our `app.component.ts` file: 

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
This is the component that makes it all possible for us to see what we get when we run the application.

Below we can see the app component structure:

<kbd>
  <img src="https://github.com/MinenhleNkosi/AngularMastery/blob/main/2.%20Create%20First%20Component/Images/0.png" height="auto" width="800" />
</kbd>
<hr>

We can see that the component is made up of three (3) files `app.component.css`, `app.component.html`, and `app.component.ts`.

That's the standard in angular, you create components as seperate files thus components are just multiple files working together that form an overall component.

## Let's add a header compoenent.
On our `app` folder, we will add a new file called `header.component.ts`:

<kbd>
  <img src="https://github.com/MinenhleNkosi/AngularMastery/blob/main/2.%20Create%20First%20Component/Images/1.png" height="auto" width="800" />
</kbd>
<hr>

Now we have created the file, in that file we need to have a **class** because components in angular are classes that are enhanced by the component decorator like the one below:

```ts
    @Component({
    selector: 'app-root',
    standalone: true,
    imports: [RouterOutlet],
    templateUrl: './app.component.html',
    styleUrl: './app.component.scss'
    })
```

Therefore in our header file I will start by exporting a new class and the class must be exported so that it can be used in other files as well. Then after that we need to have the decorator:

```ts
    import { Component } from "@angular/core";

    @Component({
        selector: 'app-root',
        standalone: true,
        imports: [],
        templateUrl: './app.component.html',
        styleUrl: './app.component.css',
    })
    export class AppComponent {}
```

On our decorator, the `selector` will let angular know which component should be controlled/replaced by our own component. So instead of the above code for the selector, the decorator will be as below:

```ts
    selector: 'app-header',
```
We use this `app-header` style to avoid builtin component clashes.

Now for our structure of the header component we have to create a file for that. We will name the file `header.component.html`. Now to link the `header.component.html` file to the decorator we will have to define the relative path to the `templateUrl` property:

```ts
    template: './header.component.html',
```

With that we can now put our markup into the html file:

```html
    <header>
        <h1>
            Easy Task
        </h1>
    </header>
```

We then need to add the standalone property on our decorator which should always set to `true`.

```ts
    standalone: true,
```

Our decorator will be as below:

```ts
    import { Component } from "@angular/core";

    @Component({
        selector: 'header-root',
        standalone: true,
        imports: [],
        template: './header.component.html',
        styleUrl: './header.component.css',
    })
    export class HeaderComponent {}
```

## Using our custom header component.
If we run the app now, the new changes we made (of the header component) will not appear on the UI since angular does not go through file to file to check if there is any new component created thus we have to explicitly tell Angular to pay attention to our new header component.

### Let's look at example of what we just said above
If we look at the `main.ts` file:

```ts
    import { bootstrapApplication } from '@angular/platform-browser';
    import { appConfig } from './app/app.config';
    import { AppComponent } from './app/app.component';

    bootstrapApplication(AppComponent, appConfig)
    .catch((err) => console.error(err));
```
With the help of the bootstrap application `bootstrapApplication(AppComponent).catch((err) => console.error(err))` function, which tells angular that there is an `AppComponent` and it should look for this `AppComponent` tag in the `index.html` file to display the content of this component on the screen.
Now that we have that information, we can actually inject another bootstrap application function which we will use to pass the `HeaderComponent` which will have a tag on the `index.html` file that will be rendered on the screen. But first we must import the `HeaderComponent` by explicitly defining the path it exists on: `import { HeaderComponent } from './app/header.component';`. The final code on `main.ts` file will be as below:

```ts
    import { bootstrapApplication } from '@angular/platform-browser';
    import { appConfig } from './app/app.config';
    import { AppComponent } from './app/app.component';
    import { HeaderComponent } from './app/header.component';

    bootstrapApplication(AppComponent, appConfig).catch((err) => console.error(err));
    bootstrapApplication(HeaderComponent, appConfig).catch((err) => console.error(err));
```

Lastly we have to add the header tag on our `index.html` file:

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
            <header-root></header-root>
            <app-root></app-root>
        </body>
    </html>
```

If we run our application we get the below:


<kbd>
  <img src="https://github.com/MinenhleNkosi/AngularMastery/blob/main/2.%20Create%20First%20Component/Images/2.png" height="auto" width="800" />
</kbd>
<hr>

Which we can see our **Easy Task** message getting displayed.

To render the *Header* component the way we did above is not the most efficient way because with angular the main objective is to build a tree of components. The root component which is the app component at the top and then there are other components that are nested inside that component or nested inside other components.

The reason for Angular team taking this approach it's because they want **data** to be exchanged quickly with each component when communicating with each other.

<kbd>
  <img src="https://github.com/MinenhleNkosi/AngularMastery/blob/main/2.%20Create%20First%20Component/Images/3.png" height="auto" width="800" />
</kbd>
<hr>

Going back to our previos code on the `main.ts` file:

```ts
    import { bootstrapApplication } from '@angular/platform-browser';
    import { appConfig } from './app/app.config';
    import { AppComponent } from './app/app.component';
    import { HeaderComponent } from './app/header.component';

    bootstrapApplication(AppComponent, appConfig).catch((err) => console.error(err));
    bootstrapApplication(HeaderComponent, appConfig).catch((err) => console.error(err));
```
We can see that there are some few changes that we need to make in order to fit the **Angular component based** standard:
1. We will have to call the `boostarpApplication()` once from the main/root component.
2. Use any other component in that **component template** or  in templates of other **nested components**.

This means we will use our **Header** component instead of the template of the **app** component.
Let's replace the *dummy* header on the starting page with the custom header component tag:

```html
    <header-root></header-root>
```

The above tag is needed since it's the tag we specified on our decorator in the `header.component` file:

```ts
    @Component({
        selector: 'header-root',
        standalone: true,
        imports: [],
        templateUrl: './header.component.html',
        styleUrl: './header.component.css',
    })
```

But after adding our tag to the `app.component.html` file, we get the below error:

<kbd>
  <img src="https://github.com/MinenhleNkosi/AngularMastery/blob/main/2.%20Create%20First%20Component/Images/4.png" height="auto" width="800" />
</kbd>
<hr>

This is because Angular does not scan all the files and folders and automatically re-adjust your components thus we must **explicitly** inform angular that we have created a new component. We do that by using a component inside of another component template. By going to the component in a template you're using in other components (which is the **app** component in our case) which is the one below:

```ts
    import { Component } from "@angular/core";

    @Component({
        selector: 'app-root',
        standalone: true,
        imports: [],
        templateUrl: './app.component.html',
        styleUrl: './app.component.css',
    })
    export class AppComponent {}
```
We now have to register that other component in the above template's component (which is the **header** component):

```ts
    import { Component } from "@angular/core";
    import { HeaderComponent} from "./header.component";

    @Component({
        selector: 'app-root',
        standalone: true,
        imports: [],
        templateUrl: './app.component.html',
        styleUrl: './app.component.css',
    })
    export class AppComponent {}
```
Now next we have to add the component to the **imports** property.

```ts
    import { Component } from "@angular/core";
    import { HeaderComponent} from "./header.component";

    @Component({
        selector: 'app-root',
        standalone: true,
        imports: [HeaderComponent],
        templateUrl: './app.component.html',
        styleUrl: './app.component.css',
    })
    export class AppComponent {}
```
Then the above will unlock the `import { HeaderComponent} from "./header.component";` component for the template of this **app** component.

Now we can save the changes and run the application to get the below results:

<kbd>
  <img src="https://github.com/MinenhleNkosi/AngularMastery/blob/main/2.%20Create%20First%20Component/Images/5.png" height="auto" width="800" />
</kbd>
<hr>










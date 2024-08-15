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

<kbd>
  <img src="https://github.com/MinenhleNkosi/AngularMastery/blob/main/1.%20Understanding%20Components%20%26%20UI/Notes/Images/0.png" height="auto" width="800" />
</kbd>
<hr>

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

<kbd>
  <img src="https://github.com/MinenhleNkosi/AngularMastery/blob/main/1.%20Understanding%20Components%20%26%20UI/Notes/Images/1.png" height="auto" width="800" />
</kbd>
<hr>

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

The template component will be located at `./app.component.html` and the code is as below:

```ts
    <style>
        :host {
            --bright-blue: oklch(51.01% 0.274 263.83);
            --electric-violet: oklch(53.18% 0.28 296.97);
            --french-violet: oklch(47.66% 0.246 305.88);
            --vivid-pink: oklch(69.02% 0.277 332.77);
            --hot-red: oklch(61.42% 0.238 15.34);
            --orange-red: oklch(63.32% 0.24 31.68);

            --gray-900: oklch(19.37% 0.006 300.98);
            --gray-700: oklch(36.98% 0.014 302.71);
            --gray-400: oklch(70.9% 0.015 304.04);

            --red-to-pink-to-purple-vertical-gradient: linear-gradient(
            180deg,
            var(--orange-red) 0%,
            var(--vivid-pink) 50%,
            var(--electric-violet) 100%
            );

            --red-to-pink-to-purple-horizontal-gradient: linear-gradient(
            90deg,
            var(--orange-red) 0%,
            var(--vivid-pink) 50%,
            var(--electric-violet) 100%
            );

            --pill-accent: var(--bright-blue);

            font-family: "Inter", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
            Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji",
            "Segoe UI Symbol";
            box-sizing: border-box;
            -webkit-font-smoothing: antialiased;
            -moz-osx-font-smoothing: grayscale;
        }

        h1 {
            font-size: 3.125rem;
            color: var(--gray-900);
            font-weight: 500;
            line-height: 100%;
            letter-spacing: -0.125rem;
            margin: 0;
            font-family: "Inter Tight", -apple-system, BlinkMacSystemFont, "Segoe UI", Roboto,
            Helvetica, Arial, sans-serif, "Apple Color Emoji", "Segoe UI Emoji",
            "Segoe UI Symbol";
        }

        p {
            margin: 0;
            color: var(--gray-700);
        }

        main {
            width: 100%;
            min-height: 100%;
            display: flex;
            justify-content: center;
            align-items: center;
            padding: 1rem;
            box-sizing: inherit;
            position: relative;
        }

        .angular-logo {
            max-width: 9.2rem;
        }

        .content {
            display: flex;
            justify-content: space-around;
            width: 100%;
            max-width: 700px;
            margin-bottom: 3rem;
        }

        .content h1 {
            margin-top: 1.75rem;
        }

        .content p {
            margin-top: 1.5rem;
        }

        .divider {
            width: 1px;
            background: var(--red-to-pink-to-purple-vertical-gradient);
            margin-inline: 0.5rem;
        }

        .pill-group {
            display: flex;
            flex-direction: column;
            align-items: start;
            flex-wrap: wrap;
            gap: 1.25rem;
        }

        .pill {
            display: flex;
            align-items: center;
            --pill-accent: var(--bright-blue);
            background: color-mix(in srgb, var(--pill-accent) 5%, transparent);
            color: var(--pill-accent);
            padding-inline: 0.75rem;
            padding-block: 0.375rem;
            border-radius: 2.75rem;
            border: 0;
            transition: background 0.3s ease;
            font-family: var(--inter-font);
            font-size: 0.875rem;
            font-style: normal;
            font-weight: 500;
            line-height: 1.4rem;
            letter-spacing: -0.00875rem;
            text-decoration: none;
        }

        .pill:hover {
            background: color-mix(in srgb, var(--pill-accent) 15%, transparent);
        }

        .pill-group .pill:nth-child(6n + 1) {
            --pill-accent: var(--bright-blue);
        }
        .pill-group .pill:nth-child(6n + 2) {
            --pill-accent: var(--french-violet);
        }
        .pill-group .pill:nth-child(6n + 3),
        .pill-group .pill:nth-child(6n + 4),
        .pill-group .pill:nth-child(6n + 5) {
            --pill-accent: var(--hot-red);
        }

        .pill-group svg {
            margin-inline-start: 0.25rem;
        }

        .social-links {
            display: flex;
            align-items: center;
            gap: 0.73rem;
            margin-top: 1.5rem;
        }

        .social-links path {
            transition: fill 0.3s ease;
            fill: var(--gray-400);
        }

        .social-links a:hover svg path {
            fill: var(--gray-900);
        }

        @media screen and (max-width: 650px) {
            .content {
            flex-direction: column;
            width: max-content;
            }

            .divider {
            height: 1px;
            width: 100%;
            background: var(--red-to-pink-to-purple-horizontal-gradient);
            margin-block: 1.5rem;
            }
        }
    </style>

    <main class="main">
        <div class="content">
            <div class="left-side">
            <svg
                xmlns="http://www.w3.org/2000/svg"
                viewBox="0 0 982 239"
                fill="none"
                class="angular-logo"
            >
                <g clip-path="url(#a)">
                <defs>
                <radialGradient
                    id="c"
                    cx="0"
                    cy="0"
                    r="1"
                    gradientTransform="rotate(118.122 171.182 60.81) scale(205.794)"
                    gradientUnits="userSpaceOnUse"
                >
                    <stop stop-color="#FF41F8" />
                    <stop offset=".707" stop-color="#FF41F8" stop-opacity=".5" />
                    <stop offset="1" stop-color="#FF41F8" stop-opacity="0" />
                </radialGradient>
                <linearGradient
                    id="b"
                    x1="0"
                    x2="982"
                    y1="192"
                    y2="192"
                    gradientUnits="userSpaceOnUse"
                >
                    <stop stop-color="#F0060B" />
                    <stop offset="0" stop-color="#F0070C" />
                    <stop offset=".526" stop-color="#CC26D5" />
                    <stop offset="1" stop-color="#7702FF" />
                </linearGradient>
                <clipPath id="a"><path fill="#fff" d="M0 0h982v239H0z" /></clipPath>
                </defs>
            </svg>
            <h1>Hello, {{ title }}</h1>
            <p>Congratulations! Your app is running. 🎉</p>
            </div>
            <div class="divider" role="separator" aria-label="Divider"></div>
            <div class="right-side">
            <div class="pill-group">
                @for (item of [
                { title: 'Explore the Docs', link: 'https://angular.dev' },
                { title: 'Learn with Tutorials', link: 'https://angular.dev/tutorials' },
                { title: 'CLI Docs', link: 'https://angular.dev/tools/cli' },
                { title: 'Angular Language Service', link: 'https://angular.dev/tools/language-service' },
                { title: 'Angular DevTools', link: 'https://angular.dev/tools/devtools' },
                ]; track item.title) {
                <a
                    class="pill"
                    [href]="item.link"
                    target="_blank"
                    rel="noopener"
                >
                    <span>{{ item.title }}</span>
                    <svg
                    xmlns="http://www.w3.org/2000/svg"
                    height="14"
                    viewBox="0 -960 960 960"
                    width="14"
                    fill="currentColor"
                    >
                    <path
                        d="M200-120q-33 0-56.5-23.5T120-200v-560q0-33 23.5-56.5T200-840h280v80H200v560h560v-280h80v280q0 33-23.5 56.5T760-120H200Zm188-212-56-56 372-372H560v-80h280v280h-80v-144L388-332Z"
                    />
                    </svg>
                </a>
                }
            </div>
            <div class="social-links">
                <a
                href="https://github.com/angular/angular"
                aria-label="Github"
                target="_blank"
                rel="noopener"
                >
                </a>
                <a
                href="https://twitter.com/angular"
                aria-label="Twitter"
                target="_blank"
                rel="noopener"
                >
                <svg
                    width="24"
                    height="24"
                    viewBox="0 0 24 24"
                    fill="none"
                    xmlns="http://www.w3.org/2000/svg"
                    alt="Twitter"
                >
                    <path
                    d="M18.244 2.25h3.308l-7.227 8.26 8.502 11.24H16.17l-5.214-6.817L4.99 21.75H1.68l7.73-8.835L1.254 2.25H8.08l4.713 6.231zm-1.161 17.52h1.833L7.084 4.126H5.117z"
                    />
                </svg>
                </a>
                <a
                href="https://www.youtube.com/channel/UCbn1OgGei-DV7aSRo_HaAiw"
                aria-label="Youtube"
                target="_blank"
                rel="noopener"
                >
                </a>
            </div>
            </div>
        </div>
    </main>
    <router-outlet />
```

Which is what we see get rendered when we run the application.





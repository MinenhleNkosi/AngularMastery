# Make the application more persentable 🎇
Styling in Angular applications is crucial for several reasons:

1. **User Experience (UX)**: Good styling enhances the overall user experience by making the application visually appealing and easier to use.
2. **Consistency**: Consistent styling across different components and pages ensures a uniform look and feel, which is important for brand identity and user familiarity.
3. **Responsiveness**: Styling helps in making the application responsive, meaning it can adapt to different screen sizes and devices, providing a better experience for users on mobile, tablet, and desktop devices.
4. **Accessibility**: Proper styling can improve the accessibility of the application, making it usable for people with disabilities. This includes considerations like color contrast, font sizes, and focus indicators.
5. **Maintainability**: Well-organized and modular styles make the application easier to maintain and update. Angular supports various ways to manage styles, such as component-specific styles, global styles, and the use of preprocessors like SCSS.

## Creating the CSS file 🌈
We have to add a file to implement our styling to the header, let's name it `header.component.css`.

## Link our Style file ♨️
Now that we have created the style file for our header component, we have to link it to the `header.component.ts` file by setting up the ~styleUrl` property:

```ts
    import { Component } from "@angular/core";

    @Component({
        selector: 'header-root',
        standalone: true,
        imports: [],
        templateUrl: './header.component.html',
        styleUrls: ['./header.component.css'],
    })
    export class HeaderComponent {}
``` 

## Adding style (❁´◡`❁)
Now that everything is linked, let's write the **CSS** content in the `header.component.css` file:

```css
    header {
        display: flex;
        flex-direction: column;
        align-items: center;
        gap: 1rem;
        width: 90%;
        max-width: 50rem;
        margin: 0 auto 2rem auto;
        text-align: center;
        background: linear-gradient(
            to bottom,
            #2c0a4c,
            #450d80
        );
        padding: 1rem;
        border-bottom-right-radius: 12px;
        border-bottom-left-radius: 12px;
        box-shadow: 0 1px 8px rgba(0, 0, 0, 0.6);
    }
    
    img {
        width: 3.5rem;
        object-fit: contain;
    }
    
    h1 {
        font-size: 1.25rem;
        margin: 0;
        padding: 0;
    }
    
    p {
        margin: 0;
        font-size: 0.8rem;
        text-wrap: balance;
    }
    
    @media (min-width: 768px) {
        header {
            padding: 2rem;
        }
    
        img {
            width: 4.5rem;
        }
    
        h1 {
            font-size: 1.5rem;
            margin: 0;
            padding: 0;
        }
    }
```

## Images 
Create a folder called **Assets** in your application. We will use this folder to store images needed as we continue with the application. 

## Styles.css file 🦿
Then now we add/create a new `styles.css` file alongside `src`, `Assets`folders. This file serves as a **global** styling for the application. Meaning the style here will affect/apply to all components on the application, unlike the `header.component.css` file which will only affect what's in the header.

```css
    * {
        box-sizing: border-box;
    }
    
    html {
        height: 100%;
    }
    
    body {
        font-family: "Poppins", sans-serif;
        background: radial-gradient(circle at top left, #181023, #0b0519);
        color: #c3b3d8;
        margin: 0;
        padding: 0;
        height: 100%;
    }
```

## Updating the index.html file 🥳
We need *google fonts* and some few extension for our application, below is the updated file:

```html
    <!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="utf-8" />
    <title>EasyTrack</title>
    <base href="/" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link rel="icon" type="image/x-icon" href="favicon.ico" />
    <link rel="preconnect" href="https://fonts.googleapis.com" />
    <link rel="preconnect" href="https://fonts.gstatic.com" crossorigin />
    <link
      href="https://fonts.googleapis.com/css2?family=Poppins:wght@400;700&display=swap"
      rel="stylesheet"
    />
  </head>
  <body>
        <app-root></app-root>
  </body>
</html>
```

## Updating the header html file 🕸️
Let's also update the mockup for the `header.component.html` component file:

```html
    <header>
        <img src="src/Assets/task-management-logo.png" alt="A todo list..."/>
        <h1>
            Easy Task
        </h1>
    </header>
```

## Things to pay attention to 😉
Now when trying to load an images using it's directory path, we should check from the `angular.json` file make sure that the `assets` configuration is set:

```json
    "src/favicon.ico",
    "assets": [
        "src/Assets",
        {
        "glob": "**/*",
        "input": "public"
        }
    ],
    "styles": [
        "src/styles.css"
    ]
```

## Updating the index.html file 🦾
Now let's make our style visible on the application by updating the `header.component.html` file:

```html
    <header>
        <img src="Assets/task-management-logo.png" alt="A todo list..."/>
        <div>
            <h1>
                Easy Task
            </h1>
            <p>
                Manage your tasks with any friction..
            </p>
        </div>
    </header>
```

With all the above done, we have improved the **styling**, **adding images**, etc. The new application is the one we see below:

<kbd>
  <img src="https://github.com/MinenhleNkosi/AngularMastery/blob/main/3.%20Styling%20Header%20Component/Images/1.png" height="auto" width="800" />
</kbd>
<hr>

From the above image is good accomplishment since now we have our finished **CUSTOM COMPONENT** 😁.

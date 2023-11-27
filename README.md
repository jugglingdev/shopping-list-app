# Shopping List App

This project was completed as part of Maximilian Schwarzm&uuml;ller's course [Angular - The Complete Guide](https://pro.academind.com/courses/) in conjunction with the [Codefi CodeLabs](https://www.codelabsdash.com/) bootcamp curriculum.

## Table of Contents

- [Shopping List App](#shopping-list-app)
  - [Table of Contents](#table-of-contents)
  - [Project Overview](#project-overview)
    - [Phase 1: The Basics](#phase-1-the-basics)
    - [Phase 2: Components \& Data Binding](#phase-2-components--data-binding)
    - [Phase 3: Directives](#phase-3-directives)
    - [Phase 4: Services \& Dependency Injection](#phase-4-services--dependency-injection)
    - [Phase 5: Routing](#phase-5-routing)
    - [Phase 6: Observables](#phase-6-observables)
    - [Phase 7: Forms](#phase-7-forms)
    - [Phase 8: Http](#phase-8-http)
  - [Reflection](#reflection)
  - [Acknowledgements](#acknowledgements)

## Project Overview

The Shopping List App was completed over # phases. In each phase, I learned important Angular concepts, practiced those concepts in smaller exercises, and then applied them to the larger Shopping List App project.

### Phase 1: The Basics

To start this project, I created a new app called `Shopping List App` with the Angular CLI.  I created the following components for the app, nested as shown:

- `header`
- `recipes`
  - `recipe-detail`
  - `recipe-list`
    - `recipe-item`
- `shopping-list`
  - `shopping-edit`

Incorporating some OOP (Object Oriented Programming), I made two class files that define recipe and ingredient classes.  The first, `recipe.model.ts`, is stored within the `recipe-list` component.  The second, `ingredient.model.ts`, is stored under the `shared` folder because both the `shopping-list` and `recipes` components will use the ingredient class.  The `.model.ts` files only define their respective classes (the properties and methods to expect); they do not create an instance of a class.

I also set up the start HTML for each component with Bootstrap classes. I used several new Bootstrap classes including:

- `.container-fluid`: creates a responsive, full-width container than spans entire viewport
- `.navbar-brand`: applied to anchor element; used for website branding or logo
- `.navbar-collapse`: creates a collapsible navigation menu fo smaller screen sizes
- `.navbar-right`: aligns elements to the right side of a navbar
- `.dropdown`: creates a dropdown menu; applied to a list element or group of elements
- `.dropdown-toggle`: opens or toggles the associated dropdown menu; applied to the trigger element
- `.dropdown-menu`: displayed when the dropdown is activated; applied to the element that contains the dropdown menu items or links
- `.caret`: adds a downward-pointing caret next to a dropdown link or button
- `.clearfix`: clears floated elements; ensures the container expands to encompass floated elements inside
- `.pull-left` and `.pull-right`: float elements to the left and right within a container
- `.img-responsive`: makes an image responsive

Another small tidbit I learned was using `role="button"` on an anchor tag.  I've seen where an `<a>` tag is used as a button (versus a `<button>` tag itself), so this was a neat attribute to incorporate.

### Phase 2: Components & Data Binding

In this phase of building the Shopping List app, I added navigation, passed data with property and event binding, and added the feature to add ingredients to the shopping list.

To make the navigation functional, I added click events to `recipes` and `Shopping List` in the `header` that calls `onSelect()` and passed in either `recipe` or `shopping-list`.  Then, I output the passed string as `featureSelected`, a new `EventEmitter`.  In `app.component.html`, I added an event listener on `featureSelected` that calls `onNavigate($event)`, updating the `loadedFeature` property in `app.component.ts`.  Finally, I added `*ngIf` statements to the `app-recipes` and `app-shopping-list` elements to display the view selected by the user.

Next up was passing recipe data with property binding.  For this, I set up the code for a single `recipe-item` and `@Input() recipe: Recipe` from `recipe.model.ts`.  I then added `*ngFor` to `recipe-list` to iterate through each `recipe-item`.  I used property binding to bind the `recipe` property from `recipe-item.component.ts` to the iterable item.  From here, I used a combination of event and property binding to display the recipe details of the selected recipe.

Side note: while incorporating the features in this phase, I noticed a trend of starting with the child component and working out to the parent.  This makes a nice flow when working with these types of data binding examples.

Lastly, I added a feature to allow the user to input a name and amount for a given ingredient and add that ingredient to the shopping list.  To do so, I added local references to `nameInput` and `amountInput` in the `shopping-edit` template and set up `@ViewChild()` decorators for each in the TypeScript.  Then, I added a `(click)` event listener on the `add` button that calls `onAddItem`, emitting `newIngredient`.  The `(ingredientAdded)` listener in the `shopping-list` template then calls `onIngredientAdded`, which pushes the new ingredient to the `ingredients` array.  Both the ingredient name and amount are displayed in the list.

This phase included a lot of new dynamic parts, so it took a lot of back-and-forth to comprehend. Still, I'm starting to see patterns working with different types of data binding.  That's a plus.

### Phase 3: Directives

Next up, I created a custom directive to open and close the Manage and Manage Recipe dropdown menus.  The directive uses the `@HostListener` decorator to listen to a click event and call the `toggleOpen()` method.  This method toggles the `isOpen` property between `true` and `false`.  The directive also uses the `@HostBinding` decorator to bind to the Bootstrap class `open` to the directive property `isOpen` in order to support `toggleOpen()`.

This was a simple step and a good example of utilizing a custom directive.

### Phase 4: Services & Dependency Injection

In this step, I created two services, `recipe` and `shopping-list`, to store the recipe and ingredients arrays respectively.  Adding these services centralized the two lists and also streamlined the methods triggered by click events.  Instead of passing data child to parent, upstream multiple times, the data now goes straight to the service and out from there wherever it is needed.

One important concept from this step was, when adding ingredients to the shopping list, emitting a slice, or copy of the new array, instead of the original to ensure that the original does not get edited accidentally.  I pulled in the Observer pattern to subscribe the shopping list to the change so it displays the updated array.

Another neat concept was adding the feature to add multiple ingredients to the shopping list.  Previously, the user could only add a single ingredient name and amount to the list at a time.  However, the new feature allows the user to add all the ingredients from a given recipe to the shopping list - all thanks to both services!

### Phase 5: Routing

This phase consisted of implementing routing.  I set up routes for the Recipes and Shopping List pages, replacing previous `*ngIf` directives as well as child pages for displaying each recipe by ID and modes for creating a new recipe and editing a current recipe.

One important takeaway is that the order of the declared paths matters.  I had to put the child route `'new'` before `':id'` because Angular will match the first path.  Meaning, if you typed `/new` as the path with the order swapped, Angular would interpret `new` as the `id` and result in an error.

Another takeaway was adding the following logic to check whether the app is in edit mode or not (the default value of `editMode` is `false`):

```ts
  this.editMode = params['id'] != null;
```

I liked seeing how using routing cleaned up the code by simplifying the syntax.  Even using the `routerLinkActive` attribute kept adding the `active` class easy and straightforward for active links.

### Phase 6: Observables

In this phase, I replaced the `EventEmitters` with `Subject`.  This meant also changing the `emit` methods to `next` and storing the `Subscription` as a property.  Then, I implements `OnDestroy` to unsubscribe the observers to prevent memory leaks or unexpected side effects.

### Phase 7: Forms

This part of the project involved adding a template-driven shopping list form and a reactive recipe edit form.

One thing I liked doing was tweaking the Add button so that it would change to Update when in edit mode. This meant I didn't need to add a separate button; the text and functionality in the background would simply switch modes. A related feature was conditionally displaying the Delete button when in edit mode.

The Observer method came in handy here. I set up a `recipesChanged` subject in the `RecipesService` so that the displayed list of recipes would update any time a recipe was edited or a new recipe was added.

Another neat feature was adding an image preview when adding a new recipe - great for UI/UX.  To do this, I created a local reference of the `imagePath` and bound its value to the image `src` property. 

### Phase 8: Http

In this part of the project, I set up a backend in Firebase using Realtime Database to store data.  The DataStorage Service is responsible for both storing and fetching recipes.  Both `map` and `tap` are used in `fetchRecipes()` to correctly handle the recipe data and display it on the recipes page.

### Phase 9: Authentication & Route Protection in Angular

The next step of the project was incorporating authentication.  I added an Auth Service to handle signing up, signing in, showing error messages during login, and storing tokens to fetch and save data from the backend in Firebase.  I also used a router guard to protect the recipes page from unauthenticated access.  Finally, I updated the header content to display the appropriate navigation links based on user status.

### Phase 10: Dynamic Components

Next up is dynamic components.  Instead of displaying an error message on the page above the login form, I made the message display as a pop-up that could be clicked out of or closed.  I explored two ways of doing this:  with `*ngIf` and programmatically by creating a component factory and using a `ViewContainerRef`.

## Reflection

## Acknowledgments

Shoutout to Maximilian Schwarzm&uuml;ller for his course [Angular - The Complete Guide](https://pro.academind.com/courses/). Thank you, Max, for your hard work creating such a comprehensive course.

Another shoutout to [Codefi CodeLabs](https://www.codelabsdash.com/) for putting together this course and pulling in the best resources for learning software development. The code coaches and this semester's cohort have been awesome to work with.

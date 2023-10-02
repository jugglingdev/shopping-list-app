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

### Phase 3: Directives

### Phase 4: Services & Dependency Injection

### Phase 5: Routing

### Phase 6: Observables

### Phase 7: Forms

### Phase 8: Http

## Reflection

## Acknowledgements

Shoutout to Maximilian Schwarzm&uuml;ller for his course [Angular - The Complete Guide](https://pro.academind.com/courses/). Thank you, Max, for your hard work creating such a comprehensive course.

Another shoutout to [Codefi CodeLabs](https://www.codelabsdash.com/) for putting together this course and pulling in the best resources for learning software development. The code coaches and this semester's cohort have been awesome to work with.

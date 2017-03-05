# Javascript MV* pattern

## - MVC: model - view - controller

- A **Model** represented domain-specific data and was ignorant of the user-interface (Views and Controllers). When a model changed, it would inform its observers.

- A **View** represented **the current state of a Model**. The Observer pattern was used for letting the View know whenever the Model was updated or modified.

- Presentation was taken care of by the View, but there wasn't just a single View and Controller - a View-Controller pair was required for each section or element being displayed on the screen.

- The **Controllers** role in this pair was handling user interaction (such as key-presses and actions e.g. clicks), making decisions for the View.

### `view` ==== observe ======> `model`
### `view` <=== notify ======== `model`
### `view` ==== represent ====> `controller`

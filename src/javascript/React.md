# Components
1. container component
It is either stateful, or interact with a state store, and potentially interact with backend services.
If building a single-page application which has routes, these would usually be the entry points for the routes
2. presentational component
It is called as dumb components, or stateless components.
It is predominantly UI components which are passed in data and callbacks by container components, calling the callbacks with updated data when specified events occur.

If your application has routing, and therefore multiple container components that need to share data across the application, it can be a good idea to introduce a centralised state store.

# state management with Redux
![image](https://cdn-images-1.medium.com/max/2000/1*L1TVVf8osq1ljBq8tJuPlw.png)

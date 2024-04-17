# 📦 Dependencies

Using third-party packages can be great within your project. Who wants to reinvent the wheel when you can `npm install` it in 2 seconds? For security and performance reasons, we should think twice before using just any package.

For every new package, we must carefully check **Quality**, **Security**, and **Stability**. Below is a list of things you should consider.

**Must**

- Come from a reputable registry like NPM
- Be checked with peers within Triple
- Check if what you use from the package is simple enough to be abstracted

**Important**

- Is the package size acceptable for your project and goal?
- Is it tree-shakable?
- Does it have side effects?
- Does the package support TypeScript?
- Does it have a low number of dependencies? (and what are these dependencies?)
- Does it have a high number of stars / weekly downloads?
- Does it have a stable version? (Use of alpha and beta is discouraged)
- How large is the number of open issues in relation to the usage and age of the package?
- Are changes committed often and recent?
- What is the number of (active) collaborators?
- Does the license allow commercial use? (Or, you should get formal approval)

**Side notes**

- Handle any audit issues upon installation.
- Don't lock versions unless you really need to. Preferably use `^version`.
- Keep dependencies up to date and audited; check frequently.
- Making changes to packages is discouraged.

## Commonly used dependencies ⭐️

In our projects, packages and libraries play a crucial role in facilitating efficient and reliable code. The list of packages and libraries below serves as a reference for the commonly used dependencies across our projects.

### State Management

State represents the part of a component that is variable depending on the user’s action. It’s a JavaScript object that acts as the memory of the component, storing many of its properties. React state management, therefore, is the process of sharing data across different components.

#### Redux

Redux is a predictable state container for JavaScript applications, used in conjunction with React. Redux offers powerful debugging capabilities through its time-traveling feature, allowing developers to track and replay state changes, aiding in identifying and fixing bugs more efficiently.

##### Pros:

\+ Large Community Support
\+ Easy debugging and testing
\+ Centralized state management

##### Cons:

\- Requires you to write a lot of boilerplate code
\- Steeper learning curve
\- Overkill for simple applications

#### Recoil

The Recoil state management library is focussed on simplicity and flexibility.It's key features include atom-based state management (allowing components to subscribe to only the specific pieces of state they need), selectors for derived state and an intuitive API.

##### Pros:

\+ Fewer boilerplate code vs. Redux
\+ Simple to learn
\+ Useful for small and large applications

##### Cons:

\- Somewhat limited community support
\- Only for React

#### Zustand

Zustand is a lightweight state management library for React applications, wit a simple and minimalistic approach. It has a functional and hook-based API, making it easy to integrate and use within React component trees. It's key features include a centralized store for state management, easy state manipulation through actions, and automatic re-rendering of components based on state changes.

##### Pros:

\+ Simple API
\+ Make use of Hooks
\+ Fewer boilerplate code vs. Redux

##### Cons:

\- Lacks extended documentation
\- Only for React

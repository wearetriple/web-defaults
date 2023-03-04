Using third party packages can be a great within your project. Who wants to invent the wheel when you can `npm install` it in 2 seconds?
For security and performance reasons we should think twice before using just any package.

For every new package we must carefully check **Quality**, **Security** and **Stability**. Below is a list of things you should consider.

**Must**

- Come from reputable registry like NPM
- Be checked with peers within Triple
- Check if what you use from the package is simple enough to be abstracted

**Important**

- Is package size acceptable for your project and goal?
- Is it Tree-shakable?
- Does it have side-effects ?
- Does the package support Typescript?
- Does it have low number of dependencies? (and, what are these dependencies?)
- Does it have a high number of stars / weekly downloads ?
- Does it have a stable version? (use of alpha and beta is discouraged)
- How large is the number of open issues in relation to usage and age of the package?
- Are changes committed often and recent?
- What is the number of (active) collaborators?
- Does the license allow commercial use? (or, you should get formal approval)

**Sidenotes**

- Handle any audit issues upon installation.
- Don’t lock versions unless you really need to. Preferably use `^version`
- Keep dependencies up to date and audited, check frequently.
- Making changes to packages is discouraged.

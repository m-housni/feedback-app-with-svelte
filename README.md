# Feedback App Using data Forwarding

![](screenshots/2021-10-25-12-54-59.png)

# Project Tree

```
rating-system-svelte
├─ .git :::> . git folder contains all the information that is necessary for your project in version control and all the information about commits, remote repository address, etc. All of them are present in this folder. It also contains a log that stores your commit history so that you can roll back to history
├─ .gitignore :::> gitignore file is a text file that tells Git which files or folders to ignore in a project. A local . gitignore file is usually placed in the root directory of a project. ... gitignore file and any entries in that file will be ignored in all of your Git repositories
├─ package-lock.json :::> auto generated for any operations where npm modifies either the node_modules tree, or package.json
├─ package.json :::> The package. json file is the heart of any Node project. It records important metadata about a project which is required before publishing to NPM, and also defines functional attributes of a project that npm uses to install dependencies, run scripts, and identify the entry point to our package
├─ public
│  ├─ build
│  │  ├─ bundle.css
│  │  ├─ bundle.js
│  │  └─ bundle.js.map
│  ├─ global.css
│  └─ index.html
├─ README.md
├─ rollup.config.js
├─ screenshots
│  └─ 2021-10-25-12-54-59.png
├─ scripts
│  └─ setupTypeScript.js
└─ src
   ├─ App.svelte
   ├─ components
   │  ├─ Card.svelte
   │  ├─ FeedbackForm.svelte
   │  ├─ FeedbackItem.svelte
   │  ├─ FeedbackList.svelte
   │  └─ RatingSelect.svelte
   └─ main.js
```
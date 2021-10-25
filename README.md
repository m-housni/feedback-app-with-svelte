# Feedback App Using data Forwarding

![](screenshots/2021-10-25-12-54-59.png)

# Project Tree

```
rating-system-svelte
├─ .git :::> for version control system (github, gitlab, bitbucked, etc)
├─ .gitignore :::> for listing the folders/files to ignore 
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
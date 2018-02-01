---
title: Introduction
seoTitle: title for search engines
seoDescription: description for search engines
isFree: true
---

## Introduction

This is an example of how content appears on this web app. Check out the table of contents on the left.

#### Export and import

Let's talk about export/import.

Consider `export default function sendEmail()`.

If our file `server/aws.js` had multiple functions to export, we would export `sendEmail()` like this:
```
function sendEmail(options) {
  // some code
}

function createTemplate(options) {
  // some code
}

export sendEmail
```

The import code may look like:
`import { sendEmail } from 'server/aws.js'`

However, in our case, `sendEmail()` is the only function that we export from `server/aws.js`, so we specify it by using `default` in our export command:
```
function sendEmail(options) {
  // some code
}

export default sendEmail
```

Or a shorter ES6 syntax :
```
export default function sendEmail(options) {
  // some code
}
```

The import code in the case of default export will be:
`import sendEmail from 'server/aws.js'`

If you'd like to give this imported function a different name (say you want to give it a more informative name in this new context), you do so with:
`import { sendEmail as sendWelcomeEmail } from 'server/sendEmail.js'`

> Del: `import { sendEmail as sendWelcomeEmail } from 'server/sendEmail.js'` is for renaming name export (not default). In order to rename default export: `import sendEmail as sendWelcomeEmail from 'server/sendEmail.js'`

In this book, I aim to keep one function per file, give that file an informative name and, as a result, use default export more frequently than standard export.

In situations where you need to use multiple API methods and maintain good modularity and readibility in your code, I suggest creating a new directory.

Let's say you have 2 AWS SES methods: `sendEmail()` and `createTemplate()`. I would create a `server/aws` folder and place 3 files in it: `sendEmail.js` (with default export of `sendEmail`), `createTemplate.js` (with default export of `createTemplate`) and `index.js`. The latter file would contain:
`server/aws/index.js` :
```
import sendEmail from 'server/aws/sendEmail';
import userApi from 'server/aws/createTemplate';

export { sendEmail, createTemplate }
```

Now you can import sendEmail() with:
`import { sendEmail } from 'server/aws'`

You can import _all_ functions with:
`import * as aws from 'server/aws'`
or
`import { sendEmail, createTemplate } from 'server/aws'`

Note that in ES6, we import from `server/aws`, not from `server/aws/index.js`.

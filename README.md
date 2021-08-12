# Avoiding Git Merge Conflicts

When you work as a team on the same project, each team member can add, edit and delete files in their own branch. You then need to merge these changes to a branch that is shared by all the team members.

Merging should be simple, but dealing with merge conflicts can be complex. So it is best to avoid merge conflicts as much as possible. Here are some tips:

## Create a separate CSS file for each page

Imagine that you have the following pages:
* Home
* UserProfile
* Jobs
* ...

You can create a `main.css` file that contains the styling that applies to every page. For example:

* Fonts
* Colours
* Styling for shared elements like the logo and a shared banner.

You can put the specific styling for the other pages in separate CSS files:

* `home.css`
* `user.css`
* `jobs.css`
* ...

Now, when you are working on one particular page, you can make changes to both the content file and the style file for that page, and your changes will not conflict with the changes made by others working on other pages.

## Writing modular code

You already have experience importing third-party modules into your JavaScript files. For example, you have often used the command:

```js
import React, {Component} from "react"
```

You can also import custom JavaScript files, to add constants or functions to a given script. For example:

```js
// utilities.jss

export const shuffle = (a) => {
  let ii = a.length

  while (ii) {
    const jj = Math.floor(Math.random() * ii)
    ii -= 1;
    [a[ii], a[jj]] = [a[jj], a[ii]]
  }

  return a // for chaining
}
```

```js
// game.js

import { shuffle } from './utilities'

const array = [1,2,3,4,5]
shuffle(array)
console.log(array)
```

```js
// possible output

> [ 2, 1, 5, 3, 4 ]
```

Breaking your scripts up into separate modules for every feature will reduce the chances that two team members will need to work on the same file at the same time. It also makes your code more robust (it is easier to ensure that each script behaves exactly as you expect it to), maintainable (it is easier to find the specific code that is causing a problem), and portable (you can easily use the same code in different places in the project and even in different projects).

## Create a shared `dev` branch

The `main` branch should be reserved for the most recent stable version of your project. It is a good idea to merge to the `main` branch only at the end of a successfully completed sprint.

For keeping track of daily changes, you can create a separate `dev` branch. The `dev` branch sis the only branch that should ever be merged to `main`; you should only merge `dev` to main at the end of a code review, where everyone has agreed that the `dev` branch is stable.

## Synchronizing your work with the `dev` branch

Each team member should be working on your own branch. Your branch should be synchronized with the `dev` branch on a regular basis, and you should merge your branch into the `dev` branch each time you reach a stable point in your work. This means that all team members can be making changes based on the same stable code.

If each team member is always working on different files from each other team member, there will never be any merge conflicts; there will never be a moment when two people make different changes to the same file.

## Handling merge conflicts

If you *do* encounter a conflict when you are merging from `dev` into your branch, or from your branch into `dev`, you can use the `git blame <filename>` [command](https://git-scm.com/docs/git-blame) to see which of your team-mates made the changes that conflict with yours. For example:

    git blame src/pages/jobs.js
    
    715b9d25 (Florin 2021-08-03 15:39:00 +0200  2) import { Container } from "react-bootstrap";
    715b9d25 (Florin 2021-08-03 15:39:00 +0200  3) 
    715b9d25 (Florin 2021-08-03 15:39:00 +0200  4) const Jobs = () => {
    715b9d25 (Florin 2021-08-03 15:39:00 +0200  5)   return (
    715b9d25 (Florin 2021-08-03 15:39:00 +0200  6)     <Container>
    715b9d25 (Florin 2021-08-03 15:39:00 +0200  7)       <div></div>
    715b9d25 (Florin 2021-08-03 15:39:00 +0200  1) import React from "react";
    715b9d25 (Florin 2021-08-03 15:39:00 +0200  8)     </Container>
    715b9d25 (Florin 2021-08-03 15:39:00 +0200  9)   );
    715b9d25 (Florin 2021-08-03 15:39:00 +0200 10) };
    715b9d25 (Florin 2021-08-03 15:39:00 +0200 11) 

You can then contact your team-mate and discuss the reasons why each of you made different changes. Together, you can decide which lines of code to keep.

You can use the Inline Action links that VS Code provides automatically, to choose which change to accept:

* Accept Current Change (in the branch that you have currently checked out)
* Accept Incoming Change (in the branch that you are merging into your current branch)
* Accept Both changes
* Compare Changes

![Inline Action Links](img/merge-conflict.png)

## Merge conflicts without any real conflict

Sometimes, you and your team-mate will have made separate changes to different parts of the same file, and both sets of changes will be valid. In this case, you can simply click on the `Accept Both Changes` inline action link.

## Further reading
https://code.visualstudio.com/docs/editor/versioncontrol

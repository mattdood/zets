---
path: '/2021/9/pages-vs-templates-in-gatsby-20210902141842'
title: 'pages vs templates in gatsby'
date: '20210902141842'
category: 'javascript'
tags: ['gatsby', 'react']
---

# pages vs templates in gatsby
I learned a valuable lesson in pages vs. templates for generating content in a
gatsby site recently.

While deploying my personal site [https://mattdood.com/](https://mattdood.com) I
wasn't able to successfully create pages using a query because it would generate
only 1 of the parent pages and ignore all `$skip` and `$limit` params passed.

This was strange, because on my local development environment it would render my
paginated content just fine.

Turns out that the issue was the `pages` vs. `templates` denomination, it attempted
to render static pages and didn't accept the query parameters. Once changing to
templates the build was able to push these params through for the pagination,
generating the content I needed.

The only change I did was to move the file from `src/pages/posts.js` -> `src/templates/posts.js`.


---
path: '/2021/8/gatsby-url-routing-20210819120217'
title: 'gatsby url routing'
date: '20210819120217'
category: 'javascript'
tags: ['gatsby', 'react']
---

# gatsby url routing
Today while drafting my personal website [mattdood.com](https://mattdood.com)
I was running into a GraphQL issue with getting my `sitePage` query to resolve
a `Path`.

This was in an effort to get my `meta` tags cobbled together for some "SEO magic".
In Django I would usually just use some `request.path` or other on the frontend,
which would dynamically resolve.

I found that there were a mixed bag of answers online, some stating we could just
place a descriptor in our `gatsby-config.js` then push that into the site via
a query and dynamically assign using the `location` "Prop". [Source](https://css-tricks.com/how-to-the-get-current-page-url-in-gatsby/).

Later this was overruled by a better approach using the backing structure of
Gatsby's routing, the React router. This allowed me to just call `location.href`
for all of my meta tag needs, a much cleaner approach. [Source](https://stackoverflow.com/a/67086455/12387496)

```javascript

import { useLocation } from '@reach/router'

const SomeComponent = () => {
  const location = useLocation()
}

// location:
// {pathname: "/", search: "", hash: "", href: "http://localhost:8000/", origin: "http://localhost:8000", …}

```


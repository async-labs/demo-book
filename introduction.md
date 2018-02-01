---
title: Introduction
seoTitle: title for search engines
seoDescription: description for search engines
isFree: true
---

## getInitialProps

`getInitialProps()` is a static method that passes data to pages (can't be used in child components) by populating `props` of page's component. In this app, we fetch data asynchronously by using `async getInitialProps()`.

`Static method` means that method defines functions that acts on [class](https://javascript.info/class) instead of particular object of the class. For example, in Chapter 6, we will introduce `pages/customer/read-chapter.js` page. Like for any page in our app which is not written as pure component, we define ES6 class as:
```
class ReadChapter extends React.Component {
  // some code
}
```

`getInitialProps()` is static method of `ReadChapter` class:
```
class ReadChapter extends React.Component {
  static async getInitialProps({ query }) {
    const { bookSlug, chapterSlug } = query;

    const chapter = await getChapterDetail({ bookSlug, chapterSlug });

    return chapter;
  }
}
```

Look at above example, user loads `pages/customer/read-chapter.js` page - `getInitialProps()` receives two slugs from `query` part of the route, passes paramaters to client-side API method `getChapterDetail()` and returns chapter `prop`. Now we are able to use chapter `prop` to show user `chapter.title` and `chapter.content`.

In above example, we pass `query` to method, but you can pass other parameters as well, check out full list of parameters in Next.js [docs](https://github.com/zeit/next.js#fetching-data-and-component-lifecycle).

As you know from our discussion of server-side rendering in Chapter 1, the optimal strategy for fast loading is render page on server for initial page load, and on client for subsequent loads. Thus, in Next.js, `getInitialProps()` executes on server for initial page load but method executes on client when user navigates via `Link` or `Router.push`.

If you want to render page on server on initial load, you should fetch data with `getInitialProps()`.

If you want page to be rendered on client, without server-side rendering for initial load, fetch data using client-side API method inside `componentDidMount` lifecycle hook.

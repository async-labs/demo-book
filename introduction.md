---
title: Introduction
seoTitle: title for search engines
seoDescription: description for search engines
isFree: true
---

## getInitialProps

### getInitialProps

#### getInitialProps

`getInitialProps()` is a static method that passes data to pages (can't be used in child components) by populating `props` of a page's component. In this app, we fetch data asynchronously by using `async getInitialProps()`.

`Static method` means that the method defines functions that act on [class](https://javascript.info/class) instead of particular object of the class. For example, in Chapter 6, we will introduce the `pages/customer/read-chapter.js` page. Like with any page in our app which is not written as a pure component, we define the ES6 class as:
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

Look at the example above. The user loads the `pages/customer/read-chapter.js` page - then `getInitialProps()` receives two slugs from the `query` part of the route, passes paramaters to the client-side API method `getChapterDetail()`, and returns chapter `prop`. Now we are able to use chapter `prop` to show the user `chapter.title` and `chapter.content`.

In this example, we pass `query` to the method, but you can pass other parameters as well. Check out the full list of parameters in Next.js [docs](https://github.com/zeit/next.js#fetching-data-and-component-lifecycle).

The optimal strategy for fast loading is rendering a page on the server for initial page load, then on the client for subsequent loads. Thus, in Next.js, `getInitialProps()` executes on the server for initial page load, but the method executes on the client when a user navigates via `Link` or `Router.push`.

If you want to render a page on the server on initial load, you should fetch data with `getInitialProps()`.

If you want the page to be rendered on client, without server-side rendering for initial load, fetch data using client-side API method inside `componentDidMount` lifecycle hook.

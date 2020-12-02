This is a starter template for [Learn Next.js](https://nextjs.org/learn).

---

# Notes for the [Official Tutorial](https://nextjs.org/learn/basics/create-nextjs-app)

[Fast reload feature doc](https://nextjs.org/docs/basic-features/fast-refresh)

- It is a tool that grows in complexity in accordance to the needs, and you can start simple.

- It was recently injected serious capitals and is going after Wordpress marketshares.

- Il fusionne NodeJS et React dans un meme ecosyteme, accelerateur de developpement

## Code splitting and prefetching

Next.js does code splitting automatically, so each page only loads what’s necessary for that page. That means when the homepage is rendered, the code [JS and CSS] for other pages is not served initially.

This ensures that the homepage loads quickly even if you add hundreds of pages.

Only loading the code for the page you request also means that pages become isolated. If a certain page throws an error, the rest of the application would still work.

Furthermore, in a production build of Next.js, whenever Link components appear in the browser’s viewport, Next.js automatically prefetches the code for the linked page in the background. By the time you click the link, the code for the destination page will already be loaded in the background, and the page transition will be near-instant!

If you need to add attributes like, for example, className, add it to the a tag, not to the Link tag.

## HTML document

If you want to customize the <html>, for example to add the lang attribute, you can do so by creating a `pages/_document.js` file. Learn more in the custom Document documentation.

## CSS

**Important:** To use CSS Modules, the CSS file name must end with .module.css.

- By default => styles-jsx [Example](https://github.com/vercel/styled-jsx) | [Doc](https://nextjs.org/docs/basic-features/built-in-css-support#adding-component-level-css)

- [To use Styled component](https://github.com/vercel/next.js/tree/canary/examples/with-styled-components)

- [SASS support](https://nextjs.org/docs/basic-features/built-in-css-support#sass-support)

- Next.js’s code splitting feature works on CSS Modules as well. It ensures the minimal amount of CSS is loaded for each page. This results in smaller bundle sizes.

CSS Modules are extracted from the JavaScript bundles at build time and generate .css files that are loaded automatically by Next.js.

### Global Styles

- CSS Modules are useful for component-level styles. But if you want some CSS to be loaded by every page, Next.js has support for that as well. It is imported from the `pages/_app.js` file.

- Its `App` component is the top-level component which will be common across all the different pages. You can use this App component to keep state when navigating between pages, for example.

- You cannot import global CSS anywhere else.

**Important:** You need to restart the development server when you add pages/\_app.js.

## About Static Generation

### Pre-rendering

**Development vs. Production**

- Generates the HTML at build time. The pre-rendered HTML is then reused on each request.
- In development (`npm run dev` or `yarn dev`), `getStaticProps` | `getStaticPaths` runs on every request.
- In production, `getStaticProps` | `getStaticPaths` runs at build time.

  _NOTE_: Because it’s meant to be run at build time, **you won’t be able to use data that’s only available during request time, such as query parameters or HTTP headers.**

  `getStaticProps` can only be exported from a page. You can’t export it from non-page files.

**What If I Need to Fetch Data at Request Time?**
_Static Generation_ is **not** a good idea if you cannot pre-render a page ahead of a user's request. Maybe your page shows frequently updated data, and the page content changes on every request.

In cases like this, you can try **Server-side Rendering** or skip pre-rendering.

### Server-side rendering

- Generates the HTML on each request.
- You need to export `getServerSideProps` instead of `getStaticProps` from your page.

## About Client-side rendering

- Statically generate (pre-render) parts of the page that do not require external data.
- When the page loads, fetch external data from the client using JavaScript and populate the remaining parts.

This approach works well for user dashboard pages, for example. Because a dashboard is a private, user-specific page, SEO is not relevant, and the page doesn’t need to be pre-rendered. The data is frequently updated, which requires request-time data fetching.

### SWR

The team behind Next.js has created a React hook for data fetching called [SWR](https://swr.vercel.app/). We highly recommend it if you’re fetching data on the client side. It handles caching, revalidation, focus tracking, refetching on interval, and more.

The name “SWR” is derived from stale-while-revalidate, a HTTP cache invalidation strategy popularized by HTTP RFC 5861. SWR is a strategy to first return the data from cache (stale), then send the fetch request (revalidate), and finally come with the up-to-date data.

https://swr.vercel.app/

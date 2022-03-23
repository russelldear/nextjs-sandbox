# Next.js stuff to remember

`<Link>` component enables client-side navigation. Create files under `/pages` and routing is set up automatically - no routing libraries
- Attributes go on the internal `<a>`, not the `<Link>`

Code-splitting happens automatically

`<Image>` component gives free image resizing & optimisation

`<Head>` lets you inject stuff into `<head>` (e.g. title)

Don't use it for external scripts though - use `<Script>`. You can set lazy loading and hook into onLoad event.  

&nbsp;  
### CSS
- Global css has to go into `pages/_app.js`  
- CSS Modules scope styles at component level  
- Sass is supported. Just add `npm install -D sass`  

&nbsp;  
### Static vs. Server-side rendering
Can render statically with build-time data by retrieving data in `getStaticProps()` function in a page, and passing the result into your default component function as a prop
- Only in next.js pages, not rando components

Rendering server-side at request time, rather than statically, implement `getServerSideProps(context)`. The `context` contains request-specific parameters  
- Also page-only
- Client-side routing still works nicely with SSR - next.js sends an API request when you navigate via `<Link>`  
- Errors in `getServerSideProps(context)` get sent to `pages/500.js` which you have to create yourself

Check out [swr](https://swr.vercel.app/) as a React hook for fetching data  

Can combine static & SSR by just fetching data from the client side

&nbsp;  
### Dynamic Routing
- Make a filename with square brackets in it - `[id].js`  
- Implement `getStaticPaths()` in that file, returning a list of objects that have `params.id`, one for each page to be built  
- Implement `getStaticProps({ params })` as above so you can get the data to be used in the page  
- `[...id].js` will give you a catch-all for things like `posts/a/b/c`. The `params.id` turns into an array of the path split by `/` 
- You can implement a custom 404 page with a file at `pages/404.js`

&nbsp;  
### API routes
API endpoints are files under `/pages/api` that implement `export default function handler(req, res)`  
`req` and `res` are just like the express ones  
Use these for runtime requests from the browser, _not_ from `getStaticProps` or `getStaticPaths` at build time 

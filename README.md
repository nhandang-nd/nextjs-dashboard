## Next.js App Router Course - Starter

This is the starter template for the Next.js App Router Course. It contains the starting code for the dashboard application.

For more information, see the [course curriculum](https://nextjs.org/learn) on the Next.js Website.

# Folder structure

- `/app`: Contains all the routes, components, and logic for your application, this is where you'll be mostly working from.
- `/app/lib`: Contains functions used in your application, such as reuseable utility functions and data fetching functions.
- `/public`: Contains all the static assets for your application, such as images
- `/scripts`: Contains a file that you'll use to populate your database
- <b>Config Files</b>: You'll also notice config files such as next.config.js at the root of your application. Most of these files are created and pre-configured when you start a new project using create-next-app.

# Style a triangle

```
<div className="h-0 w-0 border-b-[30px] border-l-[20px] border-r-[20px] border-b-black border-l-transparent border-r-transparent" />
```

# CSS Modules

Provide a way to make CSS classes locally scoped to components by default, enabling better modularity and reducing the risk of styling conflicts

# Optimizing Fonts and Images

## Why optimize fonts?

- With fonts, layout shift happens when the browser initially renders text in a fallback or system font and then swaps it out for a custom font once it has loaded. This swap can cause the text size, spacing, or layout to change, shifting elements around it.
- Next.js automatically optimizes fonts in the application when you use the `next/font` module. It does so by downloading font files at build time and hosting them with your other static assets. This means when a user visits your application, there are no additional network requests for fonts which would impact performance.

## Build Time and Runtime

<b>Build time</b> (or build step) is the name given to a series of steps that prepare your application code for production.

When you build your application, Next.js will transform your code into production-optimized files ready to be deployed to servers and consumed by users. These files include:

- HTML files for statically generated pages
- JavaScript code for rendering pages on the server
- JavaScript code for making pages interactive on the client
- CSS files

<b>Runtime</b> (or request time) refers to the period of time when your application runs in response to a user’s request, after your application has been built and deployed.

## Why optimize images?

- Ensure your image is responsive on different screen sizes.
- Specify image sizes for different devices.
  Prevent layout shift as the images load.
- Lazy load images that are outside the user's viewport.

Instead of manually handling these optimizations, you can use the next/image component to automatically optimize your images.

## The `<Image>` component

The `<Image>` Component is an extension of the HTML `<img>` tag, and comes with automatic image optimization, such as:

- Preventing layout shift automatically when images are loading.
- Resizing images to avoid shipping large images to devices with a smaller viewport.
- Lazy loading images by default (images load as they enter the viewport).
- Serving images in modern formats, like WebP and AVIF, when the browser supports it.

# Recommended reading

- [Image Optimization Docs](https://nextjs.org/docs/app/building-your-application/optimizing/images)
- [Font Optimization Docs](https://nextjs.org/docs/app/building-your-application/optimizing/fonts)
- [Improving Web Performance with Images (MDN)](https://developer.mozilla.org/en-US/docs/Learn/Performance/Multimedia)
- [Web Fonts (MDN)](https://developer.mozilla.org/en-US/docs/Learn/CSS/Styling_text/Web_fonts)

# [Layouts and Pages](https://nextjs.org/learn/dashboard-app/creating-layouts-and-pages))

# [Navigation between pages](https://nextjs.org/learn/dashboard-app/navigating-between-pages)

- [How Routing and Navigation Works](https://nextjs.org/docs/app/building-your-application/routing/linking-and-navigating#how-routing-and-navigation-works)

# [Create a repo](https://docs.github.com/en/get-started/quickstart/create-a-repo)

# What is 'seeding' in the context of databases?

Populating the database with an initial set of data

# [Route Handlers](https://nextjs.org/docs/app/building-your-application/routing/route-handlers)

[Route Segment Config](https://nextjs.org/docs/app/api-reference/file-conventions/route-segment-config#revalidate)

# [Data Fetching, Caching, and Revalidating](https://nextjs.org/docs/app/building-your-application/data-fetching/fetching-caching-and-revalidating)

# Using Server Components to fetch data

By default, Next.js applications use React Server Components, and you can opt into Client Components when needed. There are a few benefits to fetching data with React Server Components:

- Server Components execute on the server, so you can keep expensive data fetches and logic on the server and only send the result to the client.
- Server Components support promises, providing a simpler solution for asynchronous tasks like data fetching. You can use async/await syntax without reaching out for useEffect, useState or data fetching libraries.
- Since Server Components execute on the server, you can query the database directly without an additional API layer.

- You can call sql inside any Server Component. But to allow you to navigate the components more easily, we've kept all the data queries in the data.ts file, and you can import them into the components (`/app/lib/data.ts`).

# [@vercel/postgres](<(https://vercel.com/docs/storage/vercel-postgres/sdk#preventing-sql-injections)>)

# [What are request waterfalls?](https://nextjs.org/learn/dashboard-app/fetching-data#what-are-request-waterfalls)

When might you want to use a waterfall pattern?
To satisfy a condition before making the next request. For example, you might want to fetch a user's ID and profile information first. Once you have the ID, you might then proceed to fetch their list of friends.

# [Parallel data fetching](https://nextjs.org/learn/dashboard-app/fetching-data#what-are-request-waterfalls)

A common way to avoid waterfalls is to initiate all data requests at the same time - in parallel.

In JavaScript, you can use the Promise.all() or Promise.allSettled() functions to initiate all promises at the same time. For example, in data.ts, we're using Promise.all() in the fetchCardData() function:

# [Static and Dynamic Rendering](https://nextjs.org/learn/dashboard-app/static-and-dynamic-rendering)

# [Route Groups](https://nextjs.org/docs/app/building-your-application/routing/route-groups)

# [Streaming](https://nextjs.org/learn/dashboard-app/streaming)

## Deciding where to place your Suspense boundaries

Where you place your Suspense boundaries will depend on a few things:

<ol>
  <li>How you want the user to experience the page as it streams.</li>
  <li>What content you want to prioritize.</li>
  <li>If the components rely on data fetching.</li>
  <li>Take a look at your dashboard page, is there anything you would've done differently?</li>
</ol>

Don't worry. There isn't a right answer.

- You could stream the whole page like we did with loading.tsx... but that may lead to a longer loading time if one of the components has a slow data fetch.
- You could stream every component individually... but that may lead to UI popping into the screen as it becomes ready.
- You could also create a staggered effect by streaming page sections. But you'll need to create wrapper components.

Where you place your suspense boundaries will vary depending on your application. In general, it's good practice to move your data fetches down to the components that need it, and then wrap those components in Suspense. But there is nothing wrong with streaming the sections or the whole page if that's what your application needs.

Don't be afraid to experiment with Suspense and see what works best, it's a powerful API that can help you create more delightful user experiences.

### In general, what is considered good practice when working with Suspense and data fetching?

Move data fetches down to the components that need it.
By moving data fetching down to the components that need it, you can create more granular Suspense boundaries. This allows you to stream specific components and prevent the UI from blocking.

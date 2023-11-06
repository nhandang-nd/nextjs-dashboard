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

# defaultValue vs. value / Controlled vs. Uncontrolled

If you're using state to manage the value of an input, you'd use the value attribute to make it a controlled component. This means React would manage the input's state.

However, since you're not using state, you can use defaultValue. This means the native input will manage its own state. This is okay since you're saving the search query to the URL instead of state.

# ❓ When to use the useSearchParams() hook vs. the searchParams prop?

You might have noticed you used two different ways to extract search params. Whether you use one or the other depends on whether you're working on the client or the server.

`<Search>` is a Client Component, so you used the useSearchParams() hook to access the params from the client.

`<Table>` is a Server Component that fetches its own data, so you can pass the searchParams prop from the page to the component.

As a general rule, if you want to read the params from the client, use the useSearchParams() hook as this avoids having to go back to the server.

# How Debouncing Works:

1. **Trigger Event**: When an event that should be debounced (like a keystroke in the search box) occurs, a timer starts.
2. **Wait**: If a new event occurs before the timer expires, the timer is reset.
3. **Execution**: If the timer reaches the end of its countdown, the debounced function is executed.

# What are Server Actions?

React Server Actions allow you to run asynchronous code directly on the server. They eliminate the need to create API endpoints to mutate your data. Instead, you write asynchronous functions that execute on the server and can be invoked from your Client or Server Components.

Security is a top priority for web applications, as they can be vulnerable to various threats. This is where Server Actions come in. They offer an effective security solution, protecting against different types of attacks, securing your data, and ensuring authorized access. Server Actions achieve this through techniques like POST requests, encrypted closures, strict input checks, error message hashing, and host restrictions, all working together to significantly enhance your app's safety.

# Good to know:

In HTML, you'd pass a URL to the action attribute. This URL would be the destination where your form data should be submitted (usually an API endpoint).

However, in React, the action attribute is considered a special prop - meaning React builds on top of it to allow actions to be invoked. Rather than calling an API explicitly, you can pass a function to action.

Behind the scenes, Server Actions create a POST API endpoint. This is why you don't need to create API endpoints manually when using Server Actions.

# Zod

```
'use server';

import { z } from 'zod';

const InvoiceSchema = z.object({
  id: z.string(),
  customerId: z.string(),
  amount: z.coerce.number(),
  status: z.enum(['pending', 'paid']),
  date: z.string(),
});

const CreateInvoice = InvoiceSchema.omit({ id: true, date: true });

export async function createInvoice(formData: FormData) {
  // ...
}

```

# Storing values in cents

It's usually good practice to store monetary values in cents in your database to eliminate JavaScript floating-point errors and ensure greater accuracy.

```
const amountInCents = amount * 100;
```

# [Router Cache](https://nextjs.org/docs/app/building-your-application/caching#router-cache)

# Pass the id to the Server Action

Lastly, you want to pass the `id` to the Server Action so you can update the right record in your database. You cannot pass the `id` as an argument like so:

```
// Passing an id as argument won't work
<form action={updateInvoice(id)}>
```

Instead, you can pass `id` to the Server Action using JS `bind`. This will ensure that any values passed to the Server Action are encoded.

```
 const updateInvoiceWithId = updateInvoice.bind(null, invoice.id);

  return (
    <form action={updateInvoiceWithId}>
      <input type="hidden" name="id" value={invoice.id} />
    </form>
  );
```

# [error.js](https://nextjs.org/docs/app/api-reference/file-conventions/error)

There are a few things you'll notice about the code above:

- "use client" - error.tsx needs to be a Client Component.
- It accepts two props:
  - `error`: This object is an instance of JavaScript's native Error object.
  - `reset`: This is a function to reset the error boundary. When executed, the function will try to re-render the route segment.

# Server-Side validation

By validating forms on the server, you can:

- Ensure your data is in the expected format before sending it to your database.
- Reduce the risk of malicious users bypassing client-side validation.
- Have one source of truth for what is considered valid data.

# What is authentication?

Authentication is a key part of many web applications today. It's how a system checks if the user is who they say they are.

A secure website often uses multiple ways to check a user's identity for enhanced security. For instance, after entering your username and password, the site may send a verification code to your device or use an external app like Google Authenticator. This 2-factor authentication (2FA) helps increase security. Even if someone learns your password, they can't access your account without your unique token.

# Authentication vs. Authorization

In web development, authentication and authorization serve different roles:

- **Authentication** is about making sure the user is who they say they are. You're proving your identity with something you have like a username and password.
- **Authorization** is the next step. Once a user's identity is confirmed, authorization decides what parts of the application they are allowed to use.
  So, authentication checks who you are, and authorization determines what you can do or access in the application.

  [next-auth](https://authjs.dev/reference/nextjs)

# [Metadata](https://nextjs.org/learn/dashboard-app/adding-metadata)

# Resources

- [Next.js Documentation](https://nextjs.org/docs)
- [Next.js Templates](https://vercel.com/templates?framework=next.js)
- [Next.js Repository](https://github.com/vercel/next.js)
- [Vercel YouTube](https://www.youtube.com/@VercelHQ/videos)

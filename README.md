**First of all, I seriously recomend you to finish [Page Router course](https://github.com/alirezaAslani-eng/nextJs-course-page-router) before beagining this one. because you will find out the problems of `Page Router` and understand why Next.js released `App Router`**

## File System

### App Router folder structure

- The root folder `page`, now is named as `app`.

- Page components have a specific name which is `page.tsx/jsx`, that means we can not create a file like `user-info.jsx`, but instead, the structure forces us to use folders for URL segments for example :

Page router

```
|-page/
     |-products/
               |-index.tsx
               |
               |-[id].tsx
```

App router

```
|-app/
     |-products/
               |-page.tsx
               |
               |-[id]/
                     |-page.tsx
```

- now, we can access to dynamic params from component's parameter but it's a Promise and the reason is related to SRC (Server Components) which we will learn later.

```jsx
import { use } from "react";
function DynaimcPage({ params }) {
  const { id } = use(params);
  return <div>user-id {id}</div>;
}
```

### Route Group

Imagine that our project includes a larg scaled **user panel** and an **admin dashboard** but if we create all of them inside the folder `app`, we actually destroy the future of our project.

but Next.js provides a good solution to seprate our pages into several folders that are not going to be a URL sgment.

eaxample :

```
app/
   (UserPanel)/
              |-orders/
                      |-page.tsx ------ > "/orders"
```

```
app/
   (AdminPanel)/
               |-admin-panel/
                            |-payments/
                                      |-page.tsx ------ > "/admin-panel/payments"
```

### Layout and nested layout

before Next.js realesd app router, a shared ui section like navbar, topbar or a complete layout had to be be used at \_app.jsx which was the highest compoent.

but now each route or nested route can have its own layout :

```
app/
  |-layout.tsx ----- > the oldest parent layout
  |-products/
          |-page.tsx
          |-[id]/
                |-layout.js ------- > nested layout
                |-page.js
```

**NOTIC**: A nested layout must not use elements like `<html>`, `<body>`, `<head>` or any basic elements that were already existed in the oldest layout.

for example, this throws error :

```jsx
// -------- app/layout.js --------
function RootLayout({ children }) {
  return (
    <html lang="en">
      <head>
        <title>fgdfgdf</title>
      </head>
      <body>{children}</body>
    </html>
  );
}

// -------- app/products/layout.js --------
function NestedLayout({ children }) {
  return (
    <html lang="en">
      <body className="...">{children}</body>
    </html>
  );
}
```

### Route group with layout

When a user dashboard is being developed, it would probably need a complete different design for its layout, but so far we understood that if we create a layout as a nessted one it will be rendered inside the root layout `app/layout.js`, in this case we can use `Route Group` to seperate our layouts without creating a nested route :

```
app/
  |-layout.tsx ----- > Basic HTML elements (not shared ui layout)
  |
  |-(UserPanel)/
  |            |-layout.js ------- > shared ui for /tickets, /orders and /carts
  |            |
  |            |-tickets/
  |            |        |-page.tsx
  |            |
  |            |-orders/
  |            |       |-page.tsx
  |            |
  |            |-carts/
  |                   |-page.tsx
  |
  |-(AdminDashboard)/
  |                 |-layout.js ------- > shared ui for /comments, /payments and /add-product
  |                 |
  |                 |-comments/
  |                 |         |-page.tsx
  |                 |
  |                 |-payments/
  |                 |         |-page.tsx
  |                 |
  |                 |-add-product/
  |                              |-page.tsx
```
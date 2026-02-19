**First of all, I seriously recomend you to finish [Page Router course](https://github.com/alirezaAslani-eng/nextJs-course-page-router) before beagining this one. because you will find out the problems of `Page Router` and understand why Next.js released `App Router`**

## File System

### App Router folder Structure

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

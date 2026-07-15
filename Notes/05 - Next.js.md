# Next.js — Interview Preparation Guide

## Table of Contents

1. [1. What is Next.js?](#1-what-is-nextjs)
2. [2. Why was Next.js created?](#2-why-was-nextjs-created)
3. [3. Next.js vs React?](#3-nextjs-vs-react)
4. [4. What problems does Next.js solve?](#4-what-problems-does-nextjs-solve)
5. [5. What are the advantages of Next.js?](#5-what-are-the-advantages-of-nextjs)
6. [6. What are the disadvantages of Next.js?](#6-what-are-the-disadvantages-of-nextjs)
7. [7. Is Next.js frontend only?](#7-is-nextjs-frontend-only)
8. [8. What type of applications can be built with Next.js?](#8-what-type-of-applications-can-be-built-with-nextjs)
9. [9. What is the difference between SPA and Next.js apps?](#9-what-is-the-difference-between-spa-and-nextjs-apps)
10. [10. Why is Next.js good for SEO?](#10-why-is-nextjs-good-for-seo)
11. [11. What is file-based routing in Next.js?](#11-what-is-file-based-routing-in-nextjs)
12. [12. What is the App Router?](#12-what-is-the-app-router)
13. [13. What is the Pages Router?](#13-what-is-the-pages-router)
14. [14. App Router vs Pages Router?](#14-app-router-vs-pages-router)
15. [15. What is a route segment?](#15-what-is-a-route-segment)
16. [16. What is a dynamic route?](#16-what-is-a-dynamic-route)
17. [17. How do dynamic routes work in Next.js?](#17-how-do-dynamic-routes-work-in-nextjs)
18. [18. What are catch-all routes?](#18-what-are-catch-all-routes)
19. [19. What are optional catch-all routes?](#19-what-are-optional-catch-all-routes)
20. [20. What is nested routing?](#20-what-is-nested-routing)
21. [21. What is layout in Next.js App Router?](#21-what-is-layout-in-nextjs-app-router)
22. [22. What is template in Next.js?](#22-what-is-template-in-nextjs)
23. [23. What is page.tsx or page.jsx?](#23-what-is-pagetsx-or-pagejsx)
24. [24. What is loading.tsx?](#24-what-is-loadingtsx)
25. [25. What is error.tsx?](#25-what-is-errortsx)
26. [26. What is not-found.tsx?](#26-what-is-not-foundtsx)
27. [27. What is route grouping in Next.js?](#27-what-is-route-grouping-in-nextjs)
28. [28. What are parallel routes?](#28-what-are-parallel-routes)
29. [29. What are intercepting routes?](#29-what-are-intercepting-routes)
30. [30. How do you navigate between pages in Next.js?](#30-how-do-you-navigate-between-pages-in-nextjs)
31. [31. What is SSR in Next.js?](#31-what-is-ssr-in-nextjs)
32. [32. What is CSR in Next.js?](#32-what-is-csr-in-nextjs)
33. [33. What is SSG in Next.js?](#33-what-is-ssg-in-nextjs)
34. [34. What is ISR in Next.js?](#34-what-is-isr-in-nextjs)
35. [35. SSR vs SSG?](#35-ssr-vs-ssg)
36. [36. SSG vs ISR?](#36-ssg-vs-isr)
37. [37. SSR vs CSR?](#37-ssr-vs-csr)
38. [38. When should you use SSR?](#38-when-should-you-use-ssr)
39. [39. When should you use SSG?](#39-when-should-you-use-ssg)
40. [40. When should you use ISR?](#40-when-should-you-use-isr)
41. [41. What is hydration?](#41-what-is-hydration)
42. [42. What is partial hydration in Next.js context?](#42-what-is-partial-hydration-in-nextjs-context)
43. [43. What is streaming in Next.js?](#43-what-is-streaming-in-nextjs)
44. [44. Why is streaming useful?](#44-why-is-streaming-useful)
45. [45. What is progressive rendering?](#45-what-is-progressive-rendering)
46. [46. How do you fetch data in the App Router?](#46-how-do-you-fetch-data-in-the-app-router)
47. [47. How do you fetch data in the Pages Router?](#47-how-do-you-fetch-data-in-the-pages-router)
48. [48. What is getServerSideProps?](#48-what-is-getserversideprops)
49. [49. What is getStaticProps?](#49-what-is-getstaticprops)
50. [50. What is getStaticPaths?](#50-what-is-getstaticpaths)
51. [51. What is server-side data fetching?](#51-what-is-server-side-data-fetching)
52. [52. What is client-side data fetching?](#52-what-is-client-side-data-fetching)
53. [53. Which is better, server-side or client-side fetching?](#53-which-is-better-server-side-or-client-side-fetching)
54. [54. Can you use fetch directly in server components?](#54-can-you-use-fetch-directly-in-server-components)
55. [55. How does fetch caching work in Next.js?](#55-how-does-fetch-caching-work-in-nextjs)
56. [56. What is revalidate in Next.js?](#56-what-is-revalidate-in-nextjs)
57. [57. What is no-store in Next.js fetch?](#57-what-is-no-store-in-nextjs-fetch)
58. [58. What is force-cache in Next.js?](#58-what-is-force-cache-in-nextjs)
59. [59. What is on-demand revalidation?](#59-what-is-on-demand-revalidation)
60. [60. How do you handle loading and error states in Next.js?](#60-how-do-you-handle-loading-and-error-states-in-nextjs)
61. [61. What are Server Components?](#61-what-are-server-components)
62. [62. What are Client Components?](#62-what-are-client-components)
63. [63. How do you mark a Client Component?](#63-how-do-you-mark-a-client-component)
64. [64. What is the default in App Router: Server or Client Component?](#64-what-is-the-default-in-app-router-server-or-client-component)
65. [65. When should you use a Client Component?](#65-when-should-you-use-a-client-component)
66. [66. When should you use a Server Component?](#66-when-should-you-use-a-server-component)
67. [67. Can Server Components use useState or useEffect?](#67-can-server-components-use-usestate-or-useeffect)
68. [68. Can Client Components import Server Components?](#68-can-client-components-import-server-components)
69. [69. What are the benefits of Server Components?](#69-what-are-the-benefits-of-server-components)
70. [70. What are the limitations of Server Components?](#70-what-are-the-limitations-of-server-components)
71. [71. What are Server Actions?](#71-what-are-server-actions)
72. [72. Why use Server Actions?](#72-why-use-server-actions)
73. [73. How do Server Actions differ from API routes?](#73-how-do-server-actions-differ-from-api-routes)
74. [74. Can Server Actions access secrets?](#74-can-server-actions-access-secrets)
75. [75. Are Server Actions good for all mutations?](#75-are-server-actions-good-for-all-mutations)
76. [76. What is use server?](#76-what-is-use-server)
77. [77. How do forms work with Server Actions?](#77-how-do-forms-work-with-server-actions)
78. [78. What are the benefits of form actions in Next.js?](#78-what-are-the-benefits-of-form-actions-in-nextjs)
79. [79. Can Server Actions replace all backend APIs?](#79-can-server-actions-replace-all-backend-apis)
80. [80. What should you be careful about with Server Actions?](#80-what-should-you-be-careful-about-with-server-actions)
81. [81. What are API routes in Next.js?](#81-what-are-api-routes-in-nextjs)
82. [82. Where are API routes defined?](#82-where-are-api-routes-defined)
83. [83. What are route handlers in App Router?](#83-what-are-route-handlers-in-app-router)
84. [84. What HTTP methods can route handlers support?](#84-what-http-methods-can-route-handlers-support)
85. [85. When would you use API routes instead of Server Actions?](#85-when-would-you-use-api-routes-instead-of-server-actions)
86. [86. Can Next.js be used as a full backend?](#86-can-nextjs-be-used-as-a-full-backend)
87. [87. How do you connect a database in Next.js?](#87-how-do-you-connect-a-database-in-nextjs)
88. [88. Is database code safe in client components?](#88-is-database-code-safe-in-client-components)
89. [89. What is the advantage of colocating backend and frontend in Next.js?](#89-what-is-the-advantage-of-colocating-backend-and-frontend-in-nextjs)
90. [90. What is a BFF pattern and how does Next.js fit it?](#90-what-is-a-bff-pattern-and-how-does-nextjs-fit-it)
91. [91. What is middleware in Next.js?](#91-what-is-middleware-in-nextjs)
92. [92. Where does middleware run?](#92-where-does-middleware-run)
93. [93. Common use cases of middleware?](#93-common-use-cases-of-middleware)
94. [94. What is the difference between middleware and route handlers?](#94-what-is-the-difference-between-middleware-and-route-handlers)
95. [95. Should middleware do heavy business logic?](#95-should-middleware-do-heavy-business-logic)
96. [96. Why is caching important in Next.js?](#96-why-is-caching-important-in-nextjs)
97. [97. What kinds of caching exist in Next.js?](#97-what-kinds-of-caching-exist-in-nextjs)
98. [98. What is route cache?](#98-what-is-route-cache)
99. [99. What is data cache?](#99-what-is-data-cache)
100. [100. What is revalidatePath?](#100-what-is-revalidatepath)
101. [101. What is revalidateTag?](#101-what-is-revalidatetag)
102. [102. Path-based vs tag-based revalidation?](#102-path-based-vs-tag-based-revalidation)
103. [103. When should you use dynamic rendering?](#103-when-should-you-use-dynamic-rendering)
104. [104. When should you use static rendering?](#104-when-should-you-use-static-rendering)
105. [105. How do you think about caching in interviews?](#105-how-do-you-think-about-caching-in-interviews)
106. [106. What is the Next.js Image component?](#106-what-is-the-nextjs-image-component)
107. [107. Why use next/image instead of img?](#107-why-use-nextimage-instead-of-img)
108. [108. What is lazy loading in next/image?](#108-what-is-lazy-loading-in-nextimage)
109. [109. What is image optimization?](#109-what-is-image-optimization)
110. [110. What is next/font?](#110-what-is-nextfont)
111. [111. Why is font optimization important?](#111-why-is-font-optimization-important)
112. [112. How do you serve static assets in Next.js?](#112-how-do-you-serve-static-assets-in-nextjs)
113. [113. How does Next.js help with SEO?](#113-how-does-nextjs-help-with-seo)
114. [114. What is the Metadata API in Next.js?](#114-what-is-the-metadata-api-in-nextjs)
115. [115. Why is metadata important?](#115-why-is-metadata-important)
116. [116. What is Open Graph metadata?](#116-what-is-open-graph-metadata)
117. [117. Can metadata be dynamic in Next.js?](#117-can-metadata-be-dynamic-in-nextjs)
118. [118. What is the benefit of server-rendered metadata?](#118-what-is-the-benefit-of-server-rendered-metadata)
119. [119. What is Link in Next.js?](#119-what-is-link-in-nextjs)
120. [120. Why use Link instead of a normal anchor tag?](#120-why-use-link-instead-of-a-normal-anchor-tag)
121. [121. What is useRouter?](#121-what-is-userouter)
122. [122. What can you do with router.push()?](#122-what-can-you-do-with-routerpush)
123. [123. What is router.replace()?](#123-what-is-routerreplace)
124. [124. What is prefetching in Next.js?](#124-what-is-prefetching-in-nextjs)
125. [125. Is prefetching automatic in Next.js?](#125-is-prefetching-automatic-in-nextjs)
126. [126. How do you handle authentication in Next.js?](#126-how-do-you-handle-authentication-in-nextjs)
127. [127. Where should auth checks happen in Next.js?](#127-where-should-auth-checks-happen-in-nextjs)
128. [128. Can you protect routes in middleware?](#128-can-you-protect-routes-in-middleware)
129. [129. Authentication vs authorization?](#129-authentication-vs-authorization)
130. [130. Why are server-side auth checks safer?](#130-why-are-server-side-auth-checks-safer)
131. [131. How does Next.js improve performance?](#131-how-does-nextjs-improve-performance)
132. [132. What is code splitting in Next.js?](#132-what-is-code-splitting-in-nextjs)
133. [133. What is lazy loading in Next.js?](#133-what-is-lazy-loading-in-nextjs)
134. [134. How do you lazy load components in Next.js?](#134-how-do-you-lazy-load-components-in-nextjs)
135. [135. What is dynamic import in Next.js?](#135-what-is-dynamic-import-in-nextjs)
136. [136. Why are server components good for performance?](#136-why-are-server-components-good-for-performance)
137. [137. How do you optimize a slow Next.js app?](#137-how-do-you-optimize-a-slow-nextjs-app)
138. [138. How do you reduce bundle size in Next.js?](#138-how-do-you-reduce-bundle-size-in-nextjs)
139. [139. What is Web Vitals in Next.js?](#139-what-is-web-vitals-in-nextjs)
140. [140. Why does performance matter in interviews?](#140-why-does-performance-matter-in-interviews)
141. [141. Where can Next.js be deployed?](#141-where-can-nextjs-be-deployed)
142. [142. What is Edge Runtime?](#142-what-is-edge-runtime)
143. [143. Edge Runtime vs Node Runtime?](#143-edge-runtime-vs-node-runtime)
144. [144. When would you use Edge Runtime?](#144-when-would-you-use-edge-runtime)
145. [145. What are environment variables in Next.js?](#145-what-are-environment-variables-in-nextjs)
146. [146. Are all environment variables exposed to the client?](#146-are-all-environment-variables-exposed-to-the-client)
147. [147. What is the difference between build time and runtime in Next.js?](#147-what-is-the-difference-between-build-time-and-runtime-in-nextjs)
148. [148. Why does build time matter?](#148-why-does-build-time-matter)
149. [149. Can Next.js work without a backend?](#149-can-nextjs-work-without-a-backend)
150. [150. Is Next.js a full-stack framework?](#150-is-nextjs-a-full-stack-framework)
151. [151. What is hydration mismatch?](#151-what-is-hydration-mismatch)
152. [152. Common causes of hydration mismatch?](#152-common-causes-of-hydration-mismatch)
153. [153. How do you avoid hydration mismatch?](#153-how-do-you-avoid-hydration-mismatch)
154. [154. What is Suspense in Next.js?](#154-what-is-suspense-in-nextjs)
155. [155. What is streaming with Suspense?](#155-what-is-streaming-with-suspense)
156. [156. What is a rendering boundary?](#156-what-is-a-rendering-boundary)
157. [157. What is colocation in Next.js?](#157-what-is-colocation-in-nextjs)
158. [158. Why is colocation useful?](#158-why-is-colocation-useful)
159. [159. What is static export in Next.js?](#159-what-is-static-export-in-nextjs)
160. [160. Can all Next.js apps be statically exported?](#160-can-all-nextjs-apps-be-statically-exported)
161. [161. What are the major modern Next.js features?](#161-what-are-the-major-modern-nextjs-features)
162. [162. Why is the App Router considered important?](#162-why-is-the-app-router-considered-important)
163. [163. How has Next.js evolved from earlier versions?](#163-how-has-nextjs-evolved-from-earlier-versions)
164. [164. What is the significance of server-first architecture?](#164-what-is-the-significance-of-server-first-architecture)
165. [165. How do Server Actions change full-stack development?](#165-how-do-server-actions-change-full-stack-development)
166. [166. How would you choose between SSR, SSG, ISR, and CSR?](#166-how-would-you-choose-between-ssr-ssg-isr-and-csr)
167. [167. How would you structure a large Next.js application?](#167-how-would-you-structure-a-large-nextjs-application)
168. [168. How do you manage state in Next.js?](#168-how-do-you-manage-state-in-nextjs)
169. [169. How do you handle forms in modern Next.js?](#169-how-do-you-handle-forms-in-modern-nextjs)
170. [170. How do you secure a Next.js application?](#170-how-do-you-secure-a-nextjs-application)
171. [171. How do you optimize SEO in a large Next.js application?](#171-how-do-you-optimize-seo-in-a-large-nextjs-application)
172. [172. How do you handle API integration in Next.js?](#172-how-do-you-handle-api-integration-in-nextjs)
173. [173. How would you improve TTFB and LCP in Next.js?](#173-how-would-you-improve-ttfb-and-lcp-in-nextjs)
174. [174. How do you prevent unnecessary client JavaScript in Next.js?](#174-how-do-you-prevent-unnecessary-client-javascript-in-nextjs)
175. [175. What are common mistakes developers make in Next.js?](#175-what-are-common-mistakes-developers-make-in-nextjs)
176. [176. How would you explain Next.js architecture in one answer?](#176-how-would-you-explain-nextjs-architecture-in-one-answer)
177. [177. How do you debug performance issues in Next.js?](#177-how-do-you-debug-performance-issues-in-nextjs)
178. [178. How do you decide between API routes and Server Actions?](#178-how-do-you-decide-between-api-routes-and-server-actions)
179. [179. How does caching influence architecture decisions in Next.js?](#179-how-does-caching-influence-architecture-decisions-in-nextjs)
180. [180. What makes Next.js suitable for enterprise applications?](#180-what-makes-nextjs-suitable-for-enterprise-applications)
181. [Next.js vs React](#nextjs-vs-react)
182. [SSR vs SSG](#ssr-vs-ssg)
183. [SSG vs ISR](#ssg-vs-isr)
184. [CSR vs SSR](#csr-vs-ssr)
185. [App Router vs Pages Router](#app-router-vs-pages-router)
186. [Server Component vs Client Component](#server-component-vs-client-component)
187. [API Routes vs Server Actions](#api-routes-vs-server-actions)
188. [Link vs a tag](#link-vs-a-tag)
189. [revalidatePath vs revalidateTag](#revalidatepath-vs-revalidatetag)
190. [Edge Runtime vs Node Runtime](#edge-runtime-vs-node-runtime)
191. [Middleware vs Route Handler](#middleware-vs-route-handler)
192. [layout vs template](#layout-vs-template)
193. [loading.tsx vs Suspense fallback](#loadingtsx-vs-suspense-fallback)
194. [not-found.tsx vs error.tsx](#not-foundtsx-vs-errortsx)
195. [getServerSideProps vs getStaticProps](#getserversideprops-vs-getstaticprops)
196. [181. If an interviewer asks, “Explain Next.js end to end,” what would you say?](#181-if-an-interviewer-asks-explain-nextjs-end-to-end-what-would-you-say)

## 1. What is Next.js?  
**Answer:** Next.js is a React framework for building production-ready web applications. It provides features like file-based routing, server-side rendering, static site generation, API routes, image optimization, code splitting, and a strong full-stack development experience.  
  
## 2. Why was Next.js created?  
**Answer:** Next.js was created to solve the limitations of plain React in production applications, especially around routing, SEO, rendering strategies, performance optimization, and backend integration.  
  
## 3. Next.js vs React?  
**Answer:** React is a UI library for building components, while Next.js is a framework built on top of React. React handles the view layer, but Next.js adds routing, rendering strategies, API handling, optimization, and full-stack features.  
  
## 4. What problems does Next.js solve?  
**Answer:** Next.js solves common frontend problems like SEO in client-rendered apps, routing setup, code splitting, image optimization, performance issues, and the need to combine frontend and backend logic in one project.  
  
## 5. What are the advantages of Next.js?  
**Answer:** The main advantages are built-in routing, multiple rendering options like SSR and SSG, strong SEO support, automatic code splitting, server components, API routes, image optimization, and excellent integration with React.  
  
## 6. What are the disadvantages of Next.js?  
**Answer:** The main disadvantages are extra framework complexity, learning curve around rendering strategies, deployment considerations, and the fact that some features are very opinionated compared to plain React.  
  
## 7. Is Next.js frontend only?  
**Answer:** No, Next.js is not frontend only. It supports frontend rendering as well as backend capabilities like API routes, server actions, middleware, and server-side logic.  
  
## 8. What type of applications can be built with Next.js?  
**Answer:** Next.js is well suited for marketing sites, dashboards, SaaS products, e-commerce apps, blogs, content platforms, and full-stack web applications.  
  
## 9. What is the difference between SPA and Next.js apps?  
**Answer:** A traditional SPA often renders everything on the client, while Next.js gives multiple rendering options like SSR, SSG, ISR, and server components, which improves SEO and performance flexibility.  
  
## 10. Why is Next.js good for SEO?  
**Answer:** Next.js is good for SEO because it can render content on the server or at build time, so search engines receive meaningful HTML immediately instead of waiting for client-side JavaScript.  
  
---  
  
# Routing  
  
## 11. What is file-based routing in Next.js?  
**Answer:** File-based routing means routes are created automatically based on the folder and file structure. Instead of manually configuring routes, Next.js maps files to URLs.  
  
## 12. What is the App Router?  
**Answer:** The App Router is the modern routing system in Next.js based on the `app` directory. It supports nested layouts, server components, loading UI, error boundaries, streaming, and server actions.  
  
## 13. What is the Pages Router?  
**Answer:** The Pages Router is the older routing system based on the `pages` directory. It supports file-based routes and data fetching methods like `getServerSideProps` and `getStaticProps`.  
  
## 14. App Router vs Pages Router?  
**Answer:** The App Router is the newer and more powerful model with nested layouts, server components, and streaming, while the Pages Router is simpler and based on the older page-level data fetching model.  
  
## 15. What is a route segment?  
**Answer:** A route segment is one part of a route path, usually represented by one folder level in the App Router.  
  
## 16. What is a dynamic route?  
**Answer:** A dynamic route is a route where part of the URL is variable, like `[id]` or `[slug]`, allowing one route to handle many values.  
  
## 17. How do dynamic routes work in Next.js?  
**Answer:** In the file system, you define folders or files using bracket syntax like `[id]`, and Next.js passes the dynamic value through route params.  
  
## 18. What are catch-all routes?  
**Answer:** Catch-all routes use syntax like `[...slug]` to match multiple nested route segments.  
  
## 19. What are optional catch-all routes?  
**Answer:** Optional catch-all routes use syntax like `[[...slug]]` and can match both the base route and multiple nested segments.  
  
## 20. What is nested routing?  
**Answer:** Nested routing means child routes live inside parent route folders, which allows layout sharing and better route organization.  
  
## 21. What is layout in Next.js App Router?  
**Answer:** A layout is a reusable UI wrapper shared across routes. It persists across navigation and is commonly used for navigation bars, sidebars, and page structure.  
  
## 22. What is template in Next.js?  
**Answer:** A template is similar to a layout, but unlike layouts, templates re-render and remount on navigation.  
  
## 23. What is page.tsx or page.jsx?  
**Answer:** `page.tsx` or `page.jsx` defines the UI for a specific route in the App Router.  
  
## 24. What is loading.tsx?  
**Answer:** `loading.tsx` provides a loading UI for a route segment while its content is being prepared.  
  
## 25. What is error.tsx?  
**Answer:** `error.tsx` is a route-level error boundary used to display fallback UI when an error happens in that segment.  
  
## 26. What is not-found.tsx?  
**Answer:** `not-found.tsx` is used to render a custom 404-like UI when a route or resource is not found.  
  
## 27. What is route grouping in Next.js?  
**Answer:** Route groups use parentheses like `(auth)` to organize folders without affecting the URL path.  
  
## 28. What are parallel routes?  
**Answer:** Parallel routes allow multiple route segments to be rendered simultaneously in separate named slots.  
  
## 29. What are intercepting routes?  
**Answer:** Intercepting routes let one route load another route’s content in a special context, often used for modals over existing pages.  
  
## 30. How do you navigate between pages in Next.js?  
**Answer:** Navigation is usually done using the `Link` component for client-side transitions or router methods for programmatic navigation.  
  
---  
  
# Rendering Strategies  
  
## 31. What is SSR in Next.js?  
**Answer:** SSR, or server-side rendering, means the HTML is generated on the server for each request and then sent to the browser.  
  
## 32. What is CSR in Next.js?  
**Answer:** CSR, or client-side rendering, means the browser renders the UI after downloading JavaScript, often used for highly interactive parts of the app.  
  
## 33. What is SSG in Next.js?  
**Answer:** SSG, or static site generation, means HTML is generated at build time and served as static files.  
  
## 34. What is ISR in Next.js?  
**Answer:** ISR, or incremental static regeneration, allows static pages to be updated after deployment without rebuilding the whole site.  
  
## 35. SSR vs SSG?  
**Answer:** SSR renders on every request, while SSG renders once at build time. SSR is better for highly dynamic data, and SSG is better for speed and scalability when content changes less often.  
  
## 36. SSG vs ISR?  
**Answer:** SSG generates static pages once during build, while ISR allows those static pages to be refreshed later.  
  
## 37. SSR vs CSR?  
**Answer:** SSR sends rendered HTML from the server, improving SEO and initial content visibility, while CSR renders in the browser and is often better for highly interactive client-heavy experiences.  
  
## 38. When should you use SSR?  
**Answer:** I use SSR when the content must be fresh on every request, is user-specific, or is important for SEO.  
  
## 39. When should you use SSG?  
**Answer:** I use SSG for pages with mostly static content, such as blogs, marketing pages, and documentation.  
  
## 40. When should you use ISR?  
**Answer:** I use ISR when I want static performance but still need content to refresh periodically or on demand.  
  
## 41. What is hydration?  
**Answer:** Hydration is the process where React attaches event listeners and client-side behavior to server-rendered HTML.  
  
## 42. What is partial hydration in Next.js context?  
**Answer:** In modern Next.js, the idea is not exactly classic partial hydration but reducing client-side JavaScript by using server components so only the interactive parts need client behavior.  
  
## 43. What is streaming in Next.js?  
**Answer:** Streaming means sending parts of the UI to the browser as soon as they are ready instead of waiting for the whole page to finish rendering.  
  
## 44. Why is streaming useful?  
**Answer:** Streaming improves perceived performance by showing useful UI earlier, especially when some parts of the page are slower than others.  
  
## 45. What is progressive rendering?  
**Answer:** Progressive rendering means different parts of the page appear gradually as data and UI become ready, rather than all at once.  
  
---  
  
# Data Fetching  
  
## 46. How do you fetch data in the App Router?  
**Answer:** In the App Router, data fetching is often done directly inside server components using `fetch` or server-side functions, which makes the code simpler and more colocated.  
  
## 47. How do you fetch data in the Pages Router?  
**Answer:** In the Pages Router, data fetching is typically done using `getServerSideProps`, `getStaticProps`, or client-side fetching inside components.  
  
## 48. What is getServerSideProps?  
**Answer:** `getServerSideProps` is a Pages Router function that fetches data on every request and passes it as props to the page.  
  
## 49. What is getStaticProps?  
**Answer:** `getStaticProps` is a Pages Router function that fetches data at build time for static generation.  
  
## 50. What is getStaticPaths?  
**Answer:** `getStaticPaths` is used with dynamic static routes to define which paths should be pre-rendered at build time.  
  
## 51. What is server-side data fetching?  
**Answer:** Server-side data fetching means the server fetches the required data before sending HTML to the client.  
  
## 52. What is client-side data fetching?  
**Answer:** Client-side data fetching means the browser loads the page first and then fetches data using JavaScript after the component mounts.  
  
## 53. Which is better, server-side or client-side fetching?  
**Answer:** It depends on the use case. Server-side fetching is better for SEO and faster first content, while client-side fetching is useful for highly interactive or user-triggered updates.  
  
## 54. Can you use fetch directly in server components?  
**Answer:** Yes, in the App Router we can use `fetch` directly in server components, which is one of the biggest improvements in the new model.  
  
## 55. How does fetch caching work in Next.js?  
**Answer:** Next.js extends `fetch` with caching and revalidation options, allowing data to be cached, refreshed periodically, or fetched dynamically depending on configuration.  
  
## 56. What is revalidate in Next.js?  
**Answer:** `revalidate` defines after how much time a statically rendered resource should be refreshed.  
  
## 57. What is no-store in Next.js fetch?  
**Answer:** `no-store` tells Next.js not to cache the fetch result and to get fresh data every time.  
  
## 58. What is force-cache in Next.js?  
**Answer:** `force-cache` tells Next.js to cache the result and reuse it when possible.  
  
## 59. What is on-demand revalidation?  
**Answer:** On-demand revalidation is the ability to trigger content refresh manually, often after a CMS update or admin action.  
  
## 60. How do you handle loading and error states in Next.js?  
**Answer:** In the App Router, I use `loading.tsx`, `error.tsx`, and Suspense patterns. In client-side fetching, I handle loading and error state manually or through data-fetching libraries.  
  
---  
  
# Server Components & Client Components  
  
## 61. What are Server Components?  
**Answer:** Server Components are React components that run on the server. They reduce client-side JavaScript and are ideal for data fetching and non-interactive UI.  
  
## 62. What are Client Components?  
**Answer:** Client Components are components that run in the browser and are used when interactivity, state, effects, or browser APIs are needed.  
  
## 63. How do you mark a Client Component?  
**Answer:** A Client Component is marked by adding `"use client"` at the top of the file.  
  
## 64. What is the default in App Router: Server or Client Component?  
**Answer:** In the App Router, components are Server Components by default.  
  
## 65. When should you use a Client Component?  
**Answer:** I use a Client Component when I need hooks like `useState`, `useEffect`, event handlers, browser APIs, or client-only libraries.  
  
## 66. When should you use a Server Component?  
**Answer:** I use a Server Component for data fetching, static UI, secure server-side logic, and reducing unnecessary client-side bundle size.  
  
## 67. Can Server Components use useState or useEffect?  
**Answer:** No, Server Components cannot use client-side hooks like `useState` or `useEffect`.  
  
## 68. Can Client Components import Server Components?  
**Answer:** Generally, the architecture is designed so Server Components render Client Components, not the other way around in the normal direct sense.  
  
## 69. What are the benefits of Server Components?  
**Answer:** The main benefits are smaller client bundles, better performance, secure server-side logic, and easier colocated data fetching.  
  
## 70. What are the limitations of Server Components?  
**Answer:** They cannot use browser-only APIs, local interactive state hooks, or direct client event handling.  
  
---  
  
# Server Actions  
  
## 71. What are Server Actions?  
**Answer:** Server Actions are functions that run on the server and can be triggered directly from forms or UI interactions without creating a separate API route manually.  
  
## 72. Why use Server Actions?  
**Answer:** Server Actions reduce boilerplate, keep mutations closer to components, and simplify full-stack development in modern Next.js applications.  
  
## 73. How do Server Actions differ from API routes?  
**Answer:** API routes expose explicit HTTP endpoints, while Server Actions are more directly integrated into the React component model for handling server mutations.  
  
## 74. Can Server Actions access secrets?  
**Answer:** Yes, because they run on the server, they can safely access environment variables and secrets.  
  
## 75. Are Server Actions good for all mutations?  
**Answer:** They are great for many internal app mutations, especially form submissions, but API routes may still be better for public APIs or integrations.  
  
## 76. What is use server?  
**Answer:** `"use server"` marks a function or module as server-only so the logic runs on the server.  
  
## 77. How do forms work with Server Actions?  
**Answer:** A form can directly call a Server Action through the `action` prop, which simplifies submission handling.  
  
## 78. What are the benefits of form actions in Next.js?  
**Answer:** They simplify server mutations, reduce manual fetch boilerplate, and integrate well with pending and optimistic UI patterns.  
  
## 79. Can Server Actions replace all backend APIs?  
**Answer:** No, not always. They are excellent for app-internal mutations, but external consumers still need proper HTTP APIs.  
  
## 80. What should you be careful about with Server Actions?  
**Answer:** I am careful about validation, authorization, security, and understanding where the function executes so I do not accidentally mix client and server concerns.  
  
---  
  
# API Routes & Backend Features  
  
## 81. What are API routes in Next.js?  
**Answer:** API routes are backend endpoints defined inside the Next.js application, allowing server-side logic to live alongside the frontend.  
  
## 82. Where are API routes defined?  
**Answer:** In the Pages Router they are defined under `pages/api`, and in the App Router route handlers are defined using `route.ts` or `route.js`.  
  
## 83. What are route handlers in App Router?  
**Answer:** Route handlers are the App Router way of defining backend HTTP endpoints using standard request and response handling.  
  
## 84. What HTTP methods can route handlers support?  
**Answer:** Route handlers can support methods like GET, POST, PUT, PATCH, DELETE, and others depending on the needs of the API.  
  
## 85. When would you use API routes instead of Server Actions?  
**Answer:** I use API routes when I need public endpoints, third-party integrations, mobile client access, or explicit HTTP-level API architecture.  
  
## 86. Can Next.js be used as a full backend?  
**Answer:** For many applications, yes. It can handle API routes, auth flows, database access, server actions, and middleware, though very large systems may still separate backend services.  
  
## 87. How do you connect a database in Next.js?  
**Answer:** I connect a database through server-side code, such as route handlers, server actions, or server components, usually using an ORM or database client.  
  
## 88. Is database code safe in client components?  
**Answer:** No, database code should stay on the server side only.  
  
## 89. What is the advantage of colocating backend and frontend in Next.js?  
**Answer:** It improves developer productivity, reduces context switching, simplifies deployment in many cases, and keeps related logic close together.  
  
## 90. What is a BFF pattern and how does Next.js fit it?  
**Answer:** BFF stands for Backend for Frontend. Next.js fits well because it can serve as a frontend-specific backend layer handling authentication, aggregation, and client-friendly APIs.  
  
---  
  
# Middleware  
  
## 91. What is middleware in Next.js?  
**Answer:** Middleware is code that runs before a request is completed. It is used for redirects, rewrites, auth checks, localization, and other request-level logic.  
  
## 92. Where does middleware run?  
**Answer:** Middleware runs before the request reaches the route and often executes in the Edge Runtime.  
  
## 93. Common use cases of middleware?  
**Answer:** Common use cases include authentication checks, role-based redirects, A/B testing, localization, custom headers, and URL rewrites.  
  
## 94. What is the difference between middleware and route handlers?  
**Answer:** Middleware runs before route handling and can modify or redirect requests, while route handlers generate actual API responses.  
  
## 95. Should middleware do heavy business logic?  
**Answer:** No, middleware should stay lightweight because it runs on many requests and should focus on routing and request preprocessing concerns.  
  
---  
  
# Caching & Revalidation  
  
## 96. Why is caching important in Next.js?  
**Answer:** Caching improves performance, reduces server load, and helps deliver faster responses for repeated requests.  
  
## 97. What kinds of caching exist in Next.js?  
**Answer:** Next.js supports caching at multiple levels, including fetch caching, route caching, static asset caching, CDN caching, and browser caching.  
  
## 98. What is route cache?  
**Answer:** Route cache refers to caching of rendered route output so repeated access can be faster.  
  
## 99. What is data cache?  
**Answer:** Data cache stores fetched data results so they can be reused instead of being fetched repeatedly.  
  
## 100. What is revalidatePath?  
**Answer:** `revalidatePath` is used to invalidate and refresh cached content for a specific route path.  
  
## 101. What is revalidateTag?  
**Answer:** `revalidateTag` is used to invalidate cached data associated with a specific tag rather than a whole path.  
  
## 102. Path-based vs tag-based revalidation?  
**Answer:** Path-based revalidation refreshes a specific route, while tag-based revalidation is more flexible because multiple fetches can share the same tag.  
  
## 103. When should you use dynamic rendering?  
**Answer:** I use dynamic rendering when the page depends on per-request data, authentication, request headers, or fresh uncached content.  
  
## 104. When should you use static rendering?  
**Answer:** I use static rendering when the content can be reused across users and does not need to change on every request.  
  
## 105. How do you think about caching in interviews?  
**Answer:** I explain caching in terms of freshness versus performance. The correct choice depends on how often data changes, whether content is personalized, and the cost of re-rendering.  
  
---  
  
# Images, Fonts, and Assets  
  
## 106. What is the Next.js Image component?  
**Answer:** The Image component is an optimized image solution that supports responsive images, lazy loading, resizing, and modern delivery patterns.  
  
## 107. Why use next/image instead of img?  
**Answer:** `next/image` improves performance by optimizing image delivery, reducing layout shifts, and supporting responsive behavior more efficiently.  
  
## 108. What is lazy loading in next/image?  
**Answer:** Lazy loading means off-screen images are loaded only when they are about to enter the viewport.  
  
## 109. What is image optimization?  
**Answer:** Image optimization means serving correctly sized, compressed, and efficient images to improve performance and reduce bandwidth.  
  
## 110. What is next/font?  
**Answer:** `next/font` is the built-in font optimization system in Next.js that helps load fonts efficiently and reduce layout shift.  
  
## 111. Why is font optimization important?  
**Answer:** Font optimization improves performance, visual stability, and user experience by reducing unnecessary font loading delays and layout shifts.  
  
## 112. How do you serve static assets in Next.js?  
**Answer:** Static assets are commonly placed in the `public` folder and accessed directly by path.  
  
---  
  
# SEO & Metadata  
  
## 113. How does Next.js help with SEO?  
**Answer:** Next.js improves SEO with server rendering, static generation, metadata management, clean routing, and better performance.  
  
## 114. What is the Metadata API in Next.js?  
**Answer:** The Metadata API lets us define page metadata like title, description, Open Graph tags, and other SEO-related information in a structured way.  
  
## 115. Why is metadata important?  
**Answer:** Metadata is important for search engines, social sharing previews, browser tab titles, and accessibility context.  
  
## 116. What is Open Graph metadata?  
**Answer:** Open Graph metadata controls how a page appears when shared on social platforms like LinkedIn, Facebook, or others that read OG tags.  
  
## 117. Can metadata be dynamic in Next.js?  
**Answer:** Yes, metadata can be generated dynamically based on route params or fetched content.  
  
## 118. What is the benefit of server-rendered metadata?  
**Answer:** Server-rendered metadata ensures crawlers and social platforms receive correct metadata immediately.  
  
---  
  
# Navigation & Router APIs  
  
## 119. What is Link in Next.js?  
**Answer:** `Link` is the component used for client-side navigation between routes in a Next.js application.  
  
## 120. Why use Link instead of a normal anchor tag?  
**Answer:** `Link` enables client-side navigation, faster transitions, and framework-aware optimizations.  
  
## 121. What is useRouter?  
**Answer:** `useRouter` is a hook used in client components for programmatic navigation and route information.  
  
## 122. What can you do with router.push()?  
**Answer:** `router.push()` lets me navigate programmatically to another route.  
  
## 123. What is router.replace()?  
**Answer:** `router.replace()` navigates without adding a new browser history entry.  
  
## 124. What is prefetching in Next.js?  
**Answer:** Prefetching means loading route resources in advance so navigation feels faster.  
  
## 125. Is prefetching automatic in Next.js?  
**Answer:** For many cases, yes. Next.js can prefetch linked routes when appropriate.  
  
---  
  
# Authentication & Authorization  
  
## 126. How do you handle authentication in Next.js?  
**Answer:** Authentication can be handled using cookies, sessions, JWTs, auth providers, middleware, server checks, and dedicated auth libraries depending on the project architecture.  
  
## 127. Where should auth checks happen in Next.js?  
**Answer:** Auth checks should happen on the server whenever security matters, such as in middleware, route handlers, or server-rendered logic.  
  
## 128. Can you protect routes in middleware?  
**Answer:** Yes, middleware is commonly used to redirect unauthenticated users before the page loads.  
  
## 129. Authentication vs authorization?  
**Answer:** Authentication verifies who the user is, while authorization determines what the user is allowed to access.  
  
## 130. Why are server-side auth checks safer?  
**Answer:** Server-side auth checks are safer because client-side code can be manipulated, but server-side logic controls actual access to protected data.  
  
---  
  
# Performance Optimization  
  
## 131. How does Next.js improve performance?  
**Answer:** Next.js improves performance through code splitting, optimized routing, server rendering, static generation, image optimization, font optimization, caching, and server components.  
  
## 132. What is code splitting in Next.js?  
**Answer:** Code splitting means breaking JavaScript into smaller chunks so only the needed code is loaded for a route or component.  
  
## 133. What is lazy loading in Next.js?  
**Answer:** Lazy loading means loading components or resources only when they are needed.  
  
## 134. How do you lazy load components in Next.js?  
**Answer:** Components can be lazy loaded using dynamic imports.  
  
## 135. What is dynamic import in Next.js?  
**Answer:** Dynamic import allows modules or components to be loaded on demand instead of being bundled into the initial load.  
  
## 136. Why are server components good for performance?  
**Answer:** They reduce client bundle size and move more work to the server, which often improves initial load and execution performance.  
  
## 137. How do you optimize a slow Next.js app?  
**Answer:** I analyze rendering strategy, reduce client-side JavaScript, optimize images and fonts, improve caching, lazy load heavy components, profile slow data fetching, and review bundle size.  
  
## 138. How do you reduce bundle size in Next.js?  
**Answer:** I reduce bundle size by using server components where possible, lazy loading heavy libraries, removing unused dependencies, and avoiding unnecessary client-side code.  
  
## 139. What is Web Vitals in Next.js?  
**Answer:** Web Vitals are important user-centric performance metrics like LCP, CLS, and INP or FID depending on the environment.  
  
## 140. Why does performance matter in interviews?  
**Answer:** Performance matters because it affects user experience, SEO, scalability, and business metrics like conversion and retention.  
  
---  
  
# Deployment & Runtime  
  
## 141. Where can Next.js be deployed?  
**Answer:** Next.js can be deployed on platforms like Vercel, self-hosted Node environments, Docker-based setups, and various cloud providers.  
  
## 142. What is Edge Runtime?  
**Answer:** Edge Runtime allows code to run closer to users on distributed edge infrastructure, reducing latency for certain request types.  
  
## 143. Edge Runtime vs Node Runtime?  
**Answer:** The Edge Runtime is optimized for low-latency distributed execution but has a more limited API surface, while the Node runtime is more flexible and supports broader backend capabilities.  
  
## 144. When would you use Edge Runtime?  
**Answer:** I use Edge Runtime for lightweight auth checks, redirects, localization, and fast request preprocessing near the user.  
  
## 145. What are environment variables in Next.js?  
**Answer:** Environment variables store configuration like API keys, database URLs, and secrets outside the codebase.  
  
## 146. Are all environment variables exposed to the client?  
**Answer:** No. Only variables explicitly intended for the client should be exposed, while secrets must remain server-side.  
  
## 147. What is the difference between build time and runtime in Next.js?  
**Answer:** Build time happens when the app is compiled and static assets are generated, while runtime is when the app handles actual user requests.  
  
## 148. Why does build time matter?  
**Answer:** Build time matters because some pages and data can be generated in advance for faster delivery and lower runtime cost.  
  
## 149. Can Next.js work without a backend?  
**Answer:** Yes, it can consume external APIs and work as a frontend-only app, but it can also provide backend features itself.  
  
## 150. Is Next.js a full-stack framework?  
**Answer:** Yes, in modern usage Next.js is widely considered a full-stack React framework because it supports frontend and backend concerns in one system.  
  
---  
  
# Advanced Concepts  
  
## 151. What is hydration mismatch?  
**Answer:** A hydration mismatch happens when the server-rendered HTML does not match what the client expects during hydration.  
  
## 152. Common causes of hydration mismatch?  
**Answer:** Common causes include rendering random values, using browser-only APIs on the server, time-based output differences, or conditional rendering that behaves differently between server and client.  
  
## 153. How do you avoid hydration mismatch?  
**Answer:** I avoid it by keeping server and client output consistent, isolating browser-only logic to client components or effects, and avoiding unstable render-time values.  
  
## 154. What is Suspense in Next.js?  
**Answer:** Suspense is used to show fallback UI while part of the route or component tree is waiting for lazy resources or async rendering.  
  
## 155. What is streaming with Suspense?  
**Answer:** It means the server can send ready parts of the UI first and defer slower sections behind fallback boundaries.  
  
## 156. What is a rendering boundary?  
**Answer:** A rendering boundary is a part of the component tree, often defined through Suspense or route segments, that can load, fail, or stream independently.  
  
## 157. What is colocation in Next.js?  
**Answer:** Colocation means keeping route logic, data fetching, and UI close together in the same feature or route structure.  
  
## 158. Why is colocation useful?  
**Answer:** It improves maintainability, readability, and developer productivity because related logic stays together.  
  
## 159. What is static export in Next.js?  
**Answer:** Static export means generating a fully static version of the site for hosting without a Node server, though some dynamic features are limited.  
  
## 160. Can all Next.js apps be statically exported?  
**Answer:** No, apps that rely on server-only features like SSR, server actions, or certain dynamic request logic cannot always be fully exported as static sites.  
  
---  
  
# Next.js 14 / Modern Patterns  
  
## 161. What are the major modern Next.js features?  
**Answer:** The major modern features include the App Router, server components, server actions, streaming, nested layouts, route handlers, and improved caching control.  
  
## 162. Why is the App Router considered important?  
**Answer:** It simplifies full-stack React development by combining routing, layouts, data fetching, streaming, and server-first architecture in one consistent model.  
  
## 163. How has Next.js evolved from earlier versions?  
**Answer:** Earlier versions focused more on page-based rendering, while modern Next.js has become more server-first, more component-driven, and more integrated with React’s latest architecture.  
  
## 164. What is the significance of server-first architecture?  
**Answer:** Server-first architecture reduces client bundle size, improves security boundaries, and often improves initial performance and SEO.  
  
## 165. How do Server Actions change full-stack development?  
**Answer:** They reduce the need for custom mutation endpoints in many cases and make server-side mutations feel more natural inside component-driven applications.  
  
---  
  
# System Design / Senior-Level Questions  
  
## 166. How would you choose between SSR, SSG, ISR, and CSR?  
**Answer:** I choose based on freshness, personalization, SEO, and scale. If content is static, I prefer SSG. If it changes occasionally, ISR is a great fit. If it must be fresh per request, I use SSR. If the content is highly interactive and not SEO-sensitive, CSR is often enough.  
  
## 167. How would you structure a large Next.js application?  
**Answer:** I usually structure it by domain or feature, keeping route segments, components, data logic, and utilities close together. I separate shared UI, shared server utilities, and business logic clearly to avoid tight coupling.  
  
## 168. How do you manage state in Next.js?  
**Answer:** I separate state by type. Server state is preferably fetched on the server or with data libraries, local UI state stays in client components, and shared client state is handled with context or a store only when necessary.  
  
## 169. How do you handle forms in modern Next.js?  
**Answer:** In modern Next.js, I prefer form actions with Server Actions for many cases, combined with validation and good loading or optimistic UI behavior. For complex client-driven forms, I may still use a form library.  
  
## 170. How do you secure a Next.js application?  
**Answer:** I secure it by enforcing server-side authentication and authorization, validating all inputs, protecting secrets, using secure cookies and headers, avoiding trust in the client, and handling CSRF, XSS, and injection risks properly.  
  
## 171. How do you optimize SEO in a large Next.js application?  
**Answer:** I combine the right rendering strategy, strong metadata, clean semantic content, structured routing, performance optimization, and well-managed canonical and social preview tags.  
  
## 172. How do you handle API integration in Next.js?  
**Answer:** I decide first whether the API should be called from the server or client. If the data is SEO-sensitive or secret-dependent, I fetch on the server. If it is user-triggered and interactive, client fetching may be more appropriate.  
  
## 173. How would you improve TTFB and LCP in Next.js?  
**Answer:** I would reduce slow server work, optimize caching, avoid unnecessary dynamic rendering, optimize critical assets like images and fonts, and move non-essential UI or data out of the critical rendering path.  
  
## 174. How do you prevent unnecessary client JavaScript in Next.js?  
**Answer:** I keep as much UI as possible in server components, avoid marking large trees with `"use client"`, and dynamically import heavy client-only features.  
  
## 175. What are common mistakes developers make in Next.js?  
**Answer:** Common mistakes include overusing client components, misunderstanding caching, fetching data on the client unnecessarily, causing hydration mismatches, and choosing the wrong rendering strategy for the use case.  
  
## 176. How would you explain Next.js architecture in one answer?  
**Answer:** I would say Next.js is a React-based full-stack framework that combines routing, rendering, data fetching, backend capabilities, caching, and optimization features into one architecture so teams can build fast and scalable web applications with less custom setup.  
  
## 177. How do you debug performance issues in Next.js?  
**Answer:** I first identify whether the issue is server-side, network-related, or client-side. Then I inspect rendering strategy, bundle size, data-fetching latency, image and font loading, hydration cost, and route-level caching behavior.  
  
## 178. How do you decide between API routes and Server Actions?  
**Answer:** If the mutation is internal to the app and closely tied to UI forms, Server Actions are often simpler. If I need a reusable HTTP endpoint for external clients or integrations, API routes are the better choice.  
  
## 179. How does caching influence architecture decisions in Next.js?  
**Answer:** Caching changes everything because it directly affects latency, server cost, and data freshness. A good Next.js architecture always considers which data can be static, which can be revalidated, and which must stay fully dynamic.  
  
## 180. What makes Next.js suitable for enterprise applications?  
**Answer:** It is suitable because it supports scalable rendering strategies, strong performance optimization, full-stack architecture, flexible deployment, and modern React patterns, all while reducing custom infrastructure work.  
  
---  
  
# Rapid-Fire Questions  
  
## Next.js vs React  
**Answer:** React is a library; Next.js is a framework built on top of React.  
  
## SSR vs SSG  
**Answer:** SSR renders per request; SSG renders at build time.  
  
## SSG vs ISR  
**Answer:** SSG is fixed at build time; ISR allows updates after deployment.  
  
## CSR vs SSR  
**Answer:** CSR renders in the browser; SSR renders on the server.  
  
## App Router vs Pages Router  
**Answer:** App Router is the modern server-first model; Pages Router is the older page-based model.  
  
## Server Component vs Client Component  
**Answer:** Server Components run on the server; Client Components run in the browser.  
  
## API Routes vs Server Actions  
**Answer:** API routes are explicit HTTP endpoints; Server Actions are server-side functions tied closely to UI interactions.  
  
## Link vs a tag  
**Answer:** `Link` enables client-side navigation; `a` triggers normal browser navigation unless used differently.  
  
## revalidatePath vs revalidateTag  
**Answer:** `revalidatePath` refreshes a route path; `revalidateTag` refreshes tagged cached data.  
  
## Edge Runtime vs Node Runtime  
**Answer:** Edge is lightweight and distributed; Node is more flexible and feature-rich.  
  
## Middleware vs Route Handler  
**Answer:** Middleware runs before the route; route handlers generate endpoint responses.  
  
## layout vs template  
**Answer:** Layout persists across navigation; template remounts on navigation.  
  
## loading.tsx vs Suspense fallback  
**Answer:** Both show loading UI, but `loading.tsx` is route-segment based while Suspense fallback is component-boundary based.  
  
## not-found.tsx vs error.tsx  
**Answer:** `not-found.tsx` handles missing content; `error.tsx` handles runtime failures.  
  
## getServerSideProps vs getStaticProps  
**Answer:** `getServerSideProps` runs per request; `getStaticProps` runs at build time.  
  
---  
  
# Full-Interview Closing Answer  
  
## 181. If an interviewer asks, “Explain Next.js end to end,” what would you say?  
**Answer:** Next.js is a full-stack React framework designed to build fast, SEO-friendly, production-ready web applications. It gives file-based routing, multiple rendering strategies like SSR, SSG, and ISR, strong support for backend logic through API routes and Server Actions, optimization features like image and font handling, and modern React architecture with server components and streaming. What makes it powerful is that it lets us choose the right rendering and data-fetching strategy per route, so we can balance performance, SEO, freshness, and developer productivity very effectively.
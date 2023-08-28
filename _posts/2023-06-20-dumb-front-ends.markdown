---
layout: post
title:  "Web Frontends Should Be Dumb"
description: "This blog post explains why web frontends should contain as little logic as possible."
date:   2023-06-20 17:26:01 +0100
categories: software design
---
Web development has come a long way in the past twenty years. Thanks to technological improvements and a rich ecosystem, it is now possible to do almost anything in a browser. As a result, it can be tempting to build a smart (a.k.a. fat) frontend which does most of the heavy lifting in a web application. However, I think this is a bad idea and I want to explain why in this blog post.

In a web application, we can place logic in either the frontend or the backend (in the context of this blog post, the database is also considered as part of the backend). In general, we can place our logic in either layer, but there are some things which **have to be in a certain layer**:

- Validation logic and permission checks have to be in the **backend** as anything in the frontend can be manipulated at will by a malicious user.
- Localization and accessibility features need to be in the **frontend** as only it knows what the concrete device is capable of and which locale is used. This includes text orientation (left to right vs. right to left), desired date and number formats, the presence of any accessibility tools like screen readers and so on.

The decision where to put which logic has big implications on the API design: If we want to keep the frontend as thin as possible, then we need dedicated APIs which will be custom tailored for the different needs of the frontend. This is called the ["backend for frontend" pattern](https://blog.bitsrc.io/bff-pattern-backend-for-frontend-an-introduction-e4fa965128bf?gi=7edc37219b04). The opposite of this pattern would be a very thin backend where we just expose the data (including its internal structure) via some APIs and only add a minimal amount of permission checks on top. Of course, there is a continuum of compromises between these two extremes. There is no correct answer to this question as software architecture is all about tradeoffs and everything depends on the concrete situation. That said, I still recommend writing a thin frontend for these reasons:

#### Avoiding Code Duplication
Since we cannot rely on anything sent from the frontend, we have to do any calculations, validations and permission checks in the backend. If we also do them in the frontend, we end up duplicating this code which is wasteful. So, we gain a consistent business logic by doing everything in the backend. That said, we might add a small number of validations in the frontend to improve the user experience by catching obvious errors early.
#### Performance
Mobile devices are heavily used to surf the web today and while these have become incredibly powerful over the years, they are still much slower than a server. Also, they are more limited in terms of energy consumption and data bandwidth. Hence, it makes sense to assign as much work to the backend as possible to bypass these bottlenecks.
#### Easier Maintenance
If the frontend only worries about display logic, it is completely isolated from changes in the backend business logic. This allows us to change both layers independently of each other which is important as web frontend development is notoriously unstable. By having most of our code in the backend, we make it easy to switch to a different frontend technology should we wish to do so. Having a thin frontend also makes it easier to support dedicated frontends for different devices like native mobile apps as less code needs to be duplicated.
#### Easier Testing and Debugging
A clear separation of concerns between the frontend and backend simplifies automated testing and debugging. By isolating business logic in the backend, we can more easily write automated tests. Debugging becomes more straightforward, as we can concentrate on one layer at a time. If our frontend coding is thin enough, we might get away with not writing any automated tests at all for the frontend. After all, there is little point in testing the basic functionality of an UI framework.
#### Improved UI framework functionality
To keep the frontend thin, we'll need custom tailored APIs which we can build to optimally work with our frontend technology. For example, a custom [OData](https://www.odata.org/) API for a [SAP UI5](https://ui5.sap.com/) frontend reduces our frontend code to just a few lines of code. This is much easier than getting the results via a set of generic APIs and then combining and transforming these outputs to match the needs of the UI.
#### Reduced Complexity
Keeping the frontend thin allows us to spend most our [complexity budget](https://htmx.org/essays/complexity-budget/) on the backend. As the backend is the core of our application it should receive the most care to minimize complexity.

### Conclusion
There are good reasons to use a thin frontend for in web development. When in doubt, we should put logic into the backend rather than in the frontend. If you liked this blog post, please share it with somebody. You can also follow me on [Twitter/X](https://twitter.com/fxr256).
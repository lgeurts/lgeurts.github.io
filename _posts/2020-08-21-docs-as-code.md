---
layout: post
title: Docs-as-Code, when (not) to use it 
read_time: true  
comments: false
category: Education & Training
tags: [ Technical Writing ]
---

### **Hey, what do you mean with "Docs-as-Code"?**

The concept "Docs-as-Code” is basically similar to the way software engineers:
- Write code,
- Build an executable,
- Test it, and then publish the deliverable.

In technical writing terms, it can look something like:
- Store your content source in a version control system like GitHub (typically in a format like Markdown),
- Using static site generators like Middleman, Gatsby, Hugo, Jekyll, VuePress, MKDocs etc.,
- Produce a documentation site, running some validation checks (like broken links) and then publish it to your hosting provider.

### **Should I treat documentation the same as my source files?**

Source code and documentation files (even if written in MD) are not the same.

A source code file is in plain text. A compiler reads the file and converts it into a machine-readable format (like an executable file).

A documentation file on the other hand will require extra elements, such as:
- A link to an image (where will it be hosted), 
- Who is going to upload what,
- Different rich styles like Tables, Tabs, Source code viewer, etc.

In terms of source code files, compilers are pretty mature and stable. If there are syntax errors (not functional errors) the compiler will catch them immediately.

Converting Markdown (using a static code generator parser) to HTML is prone to errors. There is no defined syntax for formats like MD, merely various flavours.

### **Challenges encountered when using this approach:**

- Simple fixes are complex,
- Editorial workflow and review processes,
- Image management and preview, 
- Category management,
- Search implementation,
- When devs need to write technical docs, things can go frantic.

### **Is it worth the trouble?**

Docs differ significantly when compared to source code. In theory, it might look fascinating to go down the “Docs-as-Code” path. 

In practice it can get quite rough, especially when you're this single guy creating software documentation in a few GitHub repos, or writing some technical posts. If that's the case, I suggest skipping or you should like self-punishment.

Big companies with dedicated teams should look at tools like [docToolChain](https://doctoolchain.github.io/docToolchain/). The philosophy of docToolchain is that software documentation should be treated in the same way as code together with the [arc42 template](https://arc42.org/) for software architecture.

### **Further reading (English books)**

* [Docs Like Code (English Edition) Kindle Edition by Anne Gentle](https://www.amazon.de/dp/B0784ZJWSR)
* [Modern Technical Writing by Andrew Etter](https://www.amazon.com/Modern-Technical-Writing-Introduction-Documentation-ebook/dp/B01A2QL9SS)

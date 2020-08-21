---
layout: post
title: Docs-as-Code, my thoughts, why I use it 
read_time: true  
comments: false
category: 
tags: [ Technical Writing ]
---

**What do you mean with "Docs as Code"?**

*"Docs as code” is basically an approach similar to the way software engineers:*
- Write code,
- Build an executable,
- Test it, and then publish the deliverable.

*In technical writing terms, it can look something like:*
- Store your content source in a version control system like Github (typically in format like Markdown),
- Using a static site generator like Middleman, Gatsby, Hugo, Jekyll, VuePress, MKDocs etc.,
- Produce a documentation site, running some validation checks (like broken links) and then publish it to your hosting provider.

**Questions**

*So should you treat documentation the same as for example a source file?*

Source code and documentation files (even if written in MD) are not the same.

A source code file is in plain text. A compiler reads the file and converts it into a machine-readable format (like an executable file).

A documentation file on the other hand will require extra elements, such as:
- A link to an image (where will it be hosted), 
- Who is going to upload what,
- Different rich styles like Tables, Tabs, Source code viewer, etc.

In terms of source code files, compilers are pretty mature and stable. If there is a syntax error (not functional errors) the compiler will catch them immediately.

In contrast, converting a Markdown file (using a static code generator parser) into a final output file like HTML is error-prone. More than that there is no defined syntax for formats like Markdown, merely various flavours of it.

**Challenges I encountered when using this approach:**

- Simple fixes are complex,
- Editorial Workflow and Review processes,
- Image management and preview, 
- Category Management,
- Search Implementation,
- Developers are usually not writers. They need education.
 
 

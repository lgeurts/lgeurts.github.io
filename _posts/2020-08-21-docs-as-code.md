---
layout: post
title:“ Docs-as-Code", hype or not? 
read_time: true  
comments: false
category: 
tags: [  ]
---

**"Docs as code” is basically an approach similar to the way software engineers:**

- Write code,
- Build an executable,
- Test it, and then publish the deliverable.
- In technical writing terms, it can look something like:

In technical writing terms, it can look something like:
- Store your content source in a version control system like Github (typically in format like Markdown),
- Use a static site generator like Middleman, Gatsby, Hugo, Docusaurus, Jekyll, VuePress, MKDocs etc.,
- Produce a documentation site, running some validation checks (like broken links) and then publish it to your hosting provider.

So should you treat documentation the same as for example a source file?
For me, a source code file and a documentation file (even if it’s written in plain Markdown format) are not the same.

A source code file is in plain text. A compiler (ex: C#, Java) reads the file and converts it into a machine-readable format (like an executable file).

A documentation file on the other hand will require extra elements, such as:
- A link to an image (raising questions like, Where will it be hosted?, 
- Who is going to upload it?) and different rich styles like Tables, Tabs, Source code viewer, etc.

In terms of source code files, compilers are pretty mature and stable. If there is a syntax error (not functional errors) the compiler will catch them immediately.

In contrast, converting a Markdown file (using a static code generator parser) into a final output file like HTML is error-prone. More than that there is no defined syntax for formats like Markdown, merely various flavours of it.

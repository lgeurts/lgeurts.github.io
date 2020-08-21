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

In terms of source code files, compilers are pretty mature and stable. If there are syntax errors (not functional errors) the compiler will catch them immediately.

In contrast, converting Markdown (using a static code generator parser) to HTML is error-prone. There is no defined syntax for formats like for example MD, merely various flavours of it (yes, you are guilty too GitHub!).

**Challenges I encountered when using this approach:**

- Simple fixes are complex,
- Editorial Workflow and Review processes,
- Image management and preview, 
- Category Management,
- Search Implementation,
- Developers are usually not writers. They need education.

**Is it worth it?**

Docs differ significantly when compared to source code. In theory, it might look facinating to go down the “docs-as-code” approach, but in practice it can get quite complex, especially when you are not a single freelancer who only uses it for creating documentation in a few GitHub repos, or writing posts. The majoority of companies where there are large dedicated teams purely for documentation tend to use automated tools like 

In addition, there is an [open source tool-chain](https://doctoolchain.github.io/docToolchain/) which shows how the docs-as-code approach can be implemented.

**Further reading**

[DOCS-LIKE-CODE by Anne Gentle](https://www.amazon.de/dp/B0784ZJWSR}
[Modern Technical Writing by Andrew Etter](https://www.amazon.com/Modern-Technical-Writing-Introduction-Documentation-ebook/dp/B01A2QL9SS)


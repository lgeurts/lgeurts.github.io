Best Free Text Editor? Atom vs Vim vs Visual Studio Code

With so many programming text editors out there today, the seemingly simple task of choosing one suddenly becomes daunting and overwhelming.

While a straightforward answer to the "what is the best text editor for developers?" question doesn't exist, in this post, I will share with you a side by side comparison between four of most popular ones out there: **Atom, Sublime, Visual Studio Code, and Vim. **

After reading the list of pros and cons, I hope you will have enough information to make a choice that best fits your needs.

Disclaimer: As with any comparison, some of these views are subjective and are mostly based on my personal preferences. I'm someone who writes for the web (JS, CSS, HTML, etc.) using Sublime for Mac, so my perspective is a bit skewed towards what I'm used to. That said, I've tried to be as objective as possible.
Atom

text editor

    Url: https://atom.io/
    Cost: Free (MIT Licence)
    Developer: GitHub
    Platforms: OSX, Windows, Linux

Atom is described as:

    A hackable text editor for the 21st Century

Atom is a relative newcomer to the world of text editors but it's gained huge momentum since it was first released in 2014. Let's start by reviewing its main features:
Packages

text editor

Ability to add additional features to an edit is very important, and this is an area that Atom shines at. The package manager is installed by default and to make things even better, all packages are hosted on Github.

At the time of writing, they had a whopping 6,452 packages and themes available! Packages are so fundamental to Atom, that core features like Tree View and Settings View are simply pre-installed packages.
Editing and Workflow

In general, everything in Atom is rather smooth. Biggest pain point? Figuring out which additional packages need to be installed when starting from scratch.

For example, I like minimap to help me visually skip to parts of a file. I also needed to set up some autocompletion using Autocomplete +. I'm someone who often works on a couple of files simultaneously so the ability to set up split pane editing is a must. It's a feature Atom supports nicely.

enter image description here

Another nice feature of Atom that I've found lacking in Sublime is the drag/drop file/folder support in the tree view. I'm so used to not having it in Sublime that being able to shift things around is a real treat!

Finally, the git integration is great... it is made by GitHub after all!

Customization

Ability to customize an editor to match your development flow and style is essential. Personally, I always need to enable things like "trim whitespaces on save", "save on lost focus of file", both of which are easy to set up and override in Atom.

Atom has a great doc page on how to even override the styles (Atom's written in pure HTML/CSS on top of Chromium) - http://flight-manual.atom.io/using-atom/sections/basic-customization/

text editor

Overall, I love how configurable Atom is—ability to override settings on a per-file type basis is great! For example, different indentation for JS vs CSS vs HTML is very simple with Atom.
Performance

If there's one bone to pick with Atom, it's that at times, it feels slow. Sometimes, opening a file or switching between tabs has enough of a lag to feel painful (especially when you're in full swing development action). When I tried Atom when it was first released, performance was a problem. It has certainly gotten better since, but the frustration is still there.
Verdict

Atom is a great tool, especially for those who want to customize their editor easily, and beyond what others provide. As a web developer, the freedom to tweak, add, and extend your editor gives an incredible feeling of power. I also love its docs. The Atom Flight Manual provides a great starting point for new users.

The greatest downside for me would still be the performance issues, but for a free editor, Atom shines brightly!

text editor

    Url: https://code.visualstudio.com/
    Cost: Free
    Developer: Microsoft
    Platforms: OSX, Windows, Linux

Visual Studio Code (VSCode) is a relative newcomer to the world of text editors. It was only released last year (April 2015), but it has already been picking up a lot of traction. Microsoft has done a great job of creating a powerful and flexible cross-platform editor that's piquing a lot of interest from developers.
Packages

As with our other editors, VSCode has a nice plugin (extensions) ecosystem. The extension management is built-in, and there's already several thousands available! As with Atom, some come installed by default.

You'll need to spend some time picking out plugins that are best for your workflow. One of my favorite (and what makes me excited about VSCode) is Debugger for Chrome. It allows you to set breakpoints and debug JS from within VSCode.

text editor

The same can also be done with Node.js—setting breakpoints in VSCode and stepping through while the node process runs in a terminal.
Editing and Workflow

Although VSCode is built in a similar fashion to Atom, using Electron, Node, and HTML/CSS, it is actually much faster without any real lags.

I spent a week using the editor, and in general, I was pretty content. It had a very familiar feel to Sublime and Atom. The debugging feature mentioned above was a treat. I also set up some of the IntelliSense typeahead completion which (although painful to configure initially) started to show its benefits in a day or so. I could already whizz through typing out a function name without having to remember the arguments (or their types for that matter).

As an added bonus, the Git integration is very convenient. Not as powerful as what I get using SourceTree, but for common operations like commits and diffs, it proved to be perfect and sped up my development time.
Customization

Like the previous two editors, the expected customization features are there—all the necessary wrapping, indenting, theming, language tweaks, etc.
Performance

As mentioned before, although VSCode (like Atom) is built on Node.js, Electron, HTML, and CSS, it definitely feels fast (unlike Atom). I didn't experience any lags when opening/changing files. Searching was also fast. I believe one of the differences between Atom and VSCode is that the UI Editor is built on Monaco (from Visual Studio Online), which might be the explanation for the performance difference. In any case, the performance is definitely on par with Sublime.
Verdict

Overall I was very impressed with VSCode, to the point that I've considered moving to it more permanently. I'm still yet to take that step to fully dive in, but I think it would be a nice holiday project to configure it to meet similar standards I am used to in Sublime. After that, I think I really could stick with it for longer. The Git integration and in-editor debugger are great features that I've struggled with in Sublime but worked almost immediately in VSCode.
Vim

text editor

    Url: http://www.vim.org/
    Cost: Free GPL compatible licence
    Developer: Bram Moolenaar
    Platforms: OSX, Windows, Linux

I feel like all developers should at some point go through a "rites of passage" and use Vi or Vim for a project. Ability to edit or view a file on a remote server through a terminal is a hugely productive and important task. I've seen many developers jump through all sorts of hoops using SFTP, or curl, and re-uploading files.

However, I also recognize that the sheer mention of Vim brings shivers to some, and even righteous indignation to others. Had I omitted it, I would fear a severe smackdown from the Vim power users 😉 In all honesty for those who have spent the time to master it, it is an incredibly productive environment!
Packages

At over 14,000 packages, Vim has one for everything! Tree explorers, syntax highlighters, theming, Git integration, etc. It's all there, in multiple versions. Vim is incredibly flexible and powerful. However as with all other editors mentioned above, knowing the best plugins to install requires some insider knowledge and recommendations.

Personally, I've found going off the most popular plugins on http://vimawesome.com/ as a starting point.
Editing and Workflow

Firstly, for those not familiar with Vim, it is essentially a command line text editor. Therefore it's not some app you double click and use a mouse to move around in. The control of opening, closing, editing, saving is all keyboard shortcuts.

text editor

When I was in college, we were forced to work only in Vi for an entire module. Once you're forced to do something like that, the common keyboard commands start to become second nature. If you really want to become a Vim user, it takes real commitment, but I promise you will feel like an absolute genius by the end of it!

In all honesty, the reason I find working in Vim less efficient is because I don't know enough of the keyboard shortcuts. I can edit single files, searching, replacing, etc. with ease, but when working across multiple files, I start to lose track. So for me, Vim is a little too much.
Customization

Vim is amazingly customizable. If you Google search for .vimrc you'll find a lot of examples of preconfigured Vim configuration files. In short, anything is pretty much possible in Vim.
Performance

The only blocker to performance in Vim is the user... in other words you! It's as raw and as fast as it could be, but the performance is how quickly you can type your commands and move around! If you're a Vim power user it is blazingly fast!
Verdict

Vim is as raw of an editor as you can get. It can be an incredibly fast, efficient development environment if you can have the patience to learn the commands. There's a great online game http://vim-adventures.com/ which helps to teach the basic commands, like moving around files using h, j, k and l keys.
Final Verdict

All of the above editors have their pros and cons. Personally, I'd say that in your developer's career, you should give each one of them a shot for at least a week to see for yourself what works and what does not work for you. I hope that summarizing those four most popular text editors will make for a good starting point when considering making an editor change.

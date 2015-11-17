---
layout: post
title: Make your Jekyll Blog Awesome with Git Submodules
date: 2015-11-16 16:31:47
published: true
---

More and more people are opting for [Static Site Engines](), like [Jekyll](), for their simplicity and functionality. Jekyll allows you to turn already great Markdown into fully functioning  web pages with Liquid Tempting, SASS, and Plugins. Who doesn’t love that?

One thing you shouldn’t love is a shitty commit history littered with posts, CSS/SASS updates, and layout modifications. About 80% of all developer sites built with Jekyll have a commit history which looks like this: 

![]({{ "jekyll-commits.png" | prepend: site.images_path }})

<small> Not trying to pick on Tanner here, [mine looks even worse](https://github.com/thebearjew/thebearjew.github.io/commits/master?page=5)</small>

This is acceptable for most people because *who is the hell is going to look at the source code to your website*?!

### Why you should care
With all things, following good practice, enforcing standards, and adapting to new specifications are fundamental to being a developer. So sticking with those standards whether or not you’re getting paid, makes you a better overall programmer.

Additionally, when writing a post, story, or book, it helps to have a clear working space: be it a notebook or a computer. Interspersing your writing and developing on a personal blog makes for a messy workflow.

**Modularization**: If you’ve ever used Node.js you’ll know how awesome modules can make your life - heck any well-written library in any language makes developing a breeze. Why not take the same approach to your writing? 

Keeping your writing separate from your HTML/CSS allows you to “hot swap” the theme or structure of your Jekyll site any any time and doesn’t require checking out old commits to copy-paste old posts.

###  The Git submodule
Besides branches, commit histories, checkouts, and rebases - Git  allows for **repositories inside other repositories** called [Submodules](http://www.git-scm.com/book/en/v2/Git-Tools-Submodules).

A submodule can be added to any repository with Git’s `submodule` command. When a submodule is added, git will clone the repository in your current repository and create a `.gitmodules` file to reference the submodule going forward.

When using a submodule, we can `cd` into the directory and preform Git actions like committing, pushing, pulling, etc. without affecting the parent repository’s Git state.

### Creating a blog posts submodule
To start using a Git submodule with a Jekyll sit you first need to make a new Repository on Github and populate it with your posts.

![]({{ "blog-posts-submodule.png" | prepend: site.images_path }})

The only requirement for this repository is that it follow the  [Jekyll post naming convetion](http://jekyllrb.com/docs/posts/): YYYY-MM-DD-title-of-post.md so it can be rendered properly once we add it as a submodule to the main site.

> Make sure you’ve deleted the existing _posts/ directory originally created by Jekyll.

Lets add the blog-posts repository and simultaneously rename it to Jekyll’s native directory: _posts. 

```
git add submodule https://github.com/thebearjew/blog-posts.git _posts
Cloning into ‘_posts’…
remote: Counting objects: 11, done.
remote: Compressing objects: 100% (10/10), done.
remote: Total 11 (delta 0), reused 11 (delta 0)
Unpacking objects: 100% (11/11), done.
Checking connectivity... done.
```
<small>Note: https is required for submodules with Github Pages - [source](https://help.github.com/articles/using-submodules-with-pages/)</small>

This action does several things under the hood:

1. Creates a .gitmodules file for Git to track and manage all submodules in the parent repository.
2. Automatically changes the `:path` variable in .gitmodules to be the new path we specified - _posts
3. Adds the submodule name and url to the .git/config file in the parent repository.

Now we have to stage the newly added directory/submodule
`git add _posts` - Important: **no trailing slash**

And sync with the submodule command
`git submodules sync`

There you have it! A new directory (which is really a submodule)  to separate your writing from developing, and trick Jekyll into rendering for your site.

There’s one more thing - we need to tell git to automatically update our submodule.

### Pre-push Git hook
By default, our newly added submodule will not be automatically pulled when new commits are added. Github Pages pulls any submodules only once when the page is initially built.

A great solution is to use [Git Hooks](http://www.git-scm.com/book/en/v2/Customizing-Git-Git-Hooks) which are Bash scripts executed at specific points along the Git workflow like pre-commit, post-merge, and pre-push.
  
For our purposes, it seems to make sense to pull our submodule right before we push. When the submodule is pulled, all new commits in the submodule are treated as **one change** in the parent directory.

```
Changes not staged for commit:
  (use "git add <file>..." to update what will be committed)

  modified:   _posts (new commits)
```

This is great because we can make 10 commits to our blog-posts repository, and it will be seen as 1 commit in our parent directory (just “updating to the new HEAD for 


To add the pre-push hook, navigate into Git’s hooks directory
`cd ./git/hooks` and create a new pre-push file `vim pre-push` and add the following lines 

{% gist thebearjew/b2736e7394852ad3dd80 pre-push %}

Now when we preform any `git push` to our site, our _posts/ submodule gets updated - then look over the new updates to your posts and push the changes.

### Conclusion
That's all there is to it! I hope you find the stand-alone blog-posts submodule useful and easier with your Jekyll site. Have any suggestions, improvement, or raving reviews? Let me know: [@jryio](https:/twitter.com/jryio)

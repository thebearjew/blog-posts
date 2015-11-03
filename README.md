## Blog Posts

This separate repository containing blog posts for my blog at [jry.io](https://jry.io).

The main site is rendered and formatted using Jekyll on a [Github Pages
repository](https://github.com/thebearjew/thebearjew.github.io).

Having separate blog post and site repositories allows for making posts without
cluttering the main site repo with commits and pull requests for post updates or
spelling changes.

[Github Pages pulls submodules when building](https://help.github.com/articles/using-submodules-with-pages/) a Github Pages site, so simply
including this repository as a submodule at thebearjew.github.io is sufficient
to always have up-to-date posts.

For posts/drafts in progress, I will make branches and Pull Requests on this
repository as to not clutter the blog posts with similar edits, typos, or
drafting commits.

Let me know if you have any questions -
[@jryio](https://twitter.com/jryio).

### Adding blog posts as a submodule

- `git submodule add https://github.com/thebearjew/blog-posts`
- `mv blog-posts/ _posts/`
-  Edit `.gitmodules` file and change `path: ` variable to `_posts/`
- `git add _posts` (no trailing forward slash)
- `git submodule sync`

At this point, there is a working submodule, renamed to Jekyll's default `_posts` directory and ready render posts.

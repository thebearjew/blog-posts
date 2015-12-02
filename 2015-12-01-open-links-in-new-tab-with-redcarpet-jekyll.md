---
layout: post
title: Open External Links in New Tab - Jekyll Redcarpet
date: 2015-12-01 21:26:34
published: true
---

If you're creating a personal site or blog, you'll probably want your reader to finish your post; even when you're linkning to another site for reference. For your reader, opening a link to another site in a new tab is the best solution, and should be on by default. Here's a quick explaination & solution for your Jekyll site.

Enabling this feature within a Jekyll rendered site or blog comes down to the [Markdown renderer](http://jekyllrb.com/docs/configuration/#markdown-options) you deploy.

Jekyll supports several Markdown renderers to convert `.md` files into `.html` files, but the most used are **Kramdown**, and **Redcarpet**.

Kramdown is deployed by default, and has a feature which allows setting some links to open in a new tab using `target="_blank"`.

``` [http.cat](https://http.cat){:target="_blank"} ``` produces the following HTML `<a target="_blank" href="http://http.cat">http.cat</a>`

However, many Jekyll users are implementing Redcarpet, which provides an abundance of customizations and extensions to make specific Markdown behaviors.

The [full list]() includes code fencing, ~~strikethrough~~, _underlining_, and footnotes[^1]. These are the features you see and expect around [reddit](https://reddit.com), [Stack Overflow](http://stackoverflow.com), etc.

One drawback however, is that there is no `{:target="_blank"}` shorthand to open links in a new tab or window. Instead we can turn to JavaScript for a simple solution.


Create a new `site.js` file in your Jekyll site and link it to your primary layout (probably `default.html`) like so:

```html
[ ... html stuffs ... ]

</body>
<script type="text/javascript" src="path/to/site.js"></script>
</html>
```
First, let's write a self-executing function which will immediate call itself when the browser reachers out `<script>` tag above, and write a function called `handleLinks()`.


```js
// This function is called immediately
(function () {
  // Separate our code in case we need to do other things
  handleLinks()
})()

function handleLinks () {
}
```

Now grab all of the link elements from the HTML document using `querySelectorAll()` and loop over the NodeList.

We don't want to open links to our own site in a new tab. This is why we utilize `location.hostname` to get the host domain of the current site, in order to compare.

```js
function handleLinks () {
  var host = location.hostname // 'www.jry.io'
  var allLinks = document.querySelectorAll('a') // NodeList of all <a> elements
  for (var i = 0; i < allLinks.length; ++i) {
    // links that are not from our owns site and are not empty
    if (allLinks[i].hostname !== host && allLinks[i].hostname !== '') {
      allLinks[i].target = '_blank'
    }
  }
}
```

If you'd a modular solution, we can define our own `forEach` function for NodeLists and use it to iterate over the links.

```js
function handleExternalLinks () {
  var host = location.hostname
  var allLinks = document.querySelectorAll('a')
  forEach(allLinks, function (link, index) {
    if (link.hostname !== host && link.hostname !== '') link.target = '_blank'
  })
}

// NodeList forEach function
function forEach (nl, callback, scope) {
  for (var i = 0; i < nl.length; ++i) {
    callback.call(scope, nl[i], i)
  }
}
```

For your convenience [I've created a Gist]() of my implementation which uses RegEx to grab the "hostname" (it's a little excessive but does the same job).

That's a wrap! You're now setting all links which direct away from your own site to open in a new tab/window using `target="_blank"`. 

[^1]: Hey there's that footnote from earlier! check out [](https://reddit.com/r/dailyprogrammer) because its pretty awesome.

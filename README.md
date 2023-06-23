# Veronica Dip's Website

A website where I share information about me, my projects, and my blog.

## Serve localhost

Once you are in the directory, enter this in the terminal:

```
npx @11ty/eleventy --serve
```

## Add a file to `_site`

Add the desired file to the `.eleventy.js` export function:

```
module.exports = function (eleventyConfig) {
  // ...
  eleventyConfig.addPassthroughCopy("example.html");
};
```

## .njk files

### base.njk

The base template, all the files use this.

### blog.njk

The extra things that the blog home and the posts needs.

### home.njk

The extra things that the home page uses.

### social_footer.njk

The `<ul>` portion with all the social media links.

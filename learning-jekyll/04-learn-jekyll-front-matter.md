---
layout: page
title: "Jekyll Front Matter"
nav_order: 14
parent: "Create a Static Site Using Jekyll: Introduction"
---

# Jekyll Front Matter

Jekyll uses ["front matter"](https://jekyllrb.com/docs/step-by-step/03-front-matter/#use-front-matter){:target="_blank"} to assign properties to the markdown files in your site. The Jekyll documentation says that front matter is actually YAML. Jekyll sites must contain front matter at the top of the file. Front matter is contained in a block set off by the hyphens on their own line. The front matter for this page as I create it right now looks like this:

```yaml
---
ADD FRONT MATTER LATER
---
```

Without front matter, the Jekyll will not recognize the file as a page or post to be built as part of the site. Remember in Create a Page when I created that Contact Me page? If you've been following along and previewing the site with `jekyll serve`, you may have noticed that there is no Contact page. That's because I didn't give it any front matter. If I open `contact.md` you see it just starts with the `#` to create an h1 tag. To change this, add the most basic piece of front matter:

1. Open `contact.md`.
2. Use the `Enter` key to create several lines of white space at the top of the file.
3. On line 1, type `---`.
4. On line 2, type `layout: page`.
5. On line 3, enter a page title: `title: Contact Me`. 
5. On line 4, enter in another three hyphens: `---`.
6. Save the file.
7. Run `bundle exec jekyll serve again`
8. When you reload the page, the Contact page appears in the left sidebar and you can click on it to open the page.

Here's what `contact.md` looks like with the update:

```yaml
---
layout: page
title: Contact Me
---

# Contact Me

You can email me at [email@email.com](mailto:email@email.com).

I promise I will receive the email and get back to you.
```

To make Jekyll process a page without defining variables in the front matter, add the two lines of three hyphens each at the top of your page:

```yaml
---
---
```

Let's take the front matter a little farther an do some [Cleanup and Site and File Organization]({% link learning-jekyll/05-learn-jekyll-organization.md %})
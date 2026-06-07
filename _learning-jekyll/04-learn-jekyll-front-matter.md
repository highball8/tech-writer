---
layout: page
title: "Jekyll Front Matter"
nav_order: 14
parent: "Create a Static Site Using Jekyll: Introduction"
---

# Jekyll Front Matter

Jekyll uses ["front matter"](https://jekyllrb.com/docs/step-by-step/03-front-matter/#use-front-matter){:target="_blank"} to assign properties to the Markdown files on your site. The Jekyll documentation says that front matter is actually YAML. Jekyll sites **must** contain front matter at the top of the file. Front matter is contained in a block set off by the hyphens on their own line. The front matter for this page as I create it right now looks like this:

```yaml
---
ADD FRONT MATTER LATER
---
```

Without front matter, the Jekyll will not recognize the file as a Jekyll page or post to build so it won't function as part of your site. Anything without front matter won't be structured or styled like the rest of your site, it won't be included in categories or menus, and just will not function as part of the website.

If you have been following along, you created a Contact Me page in [Build Content for Your First Jekyll Site]({% link _learning-jekyll/03-learn-jekyll-build-content.md %}). But that page is not going to display in any site menus or any site navigation at all until you add Jekyll front matter.

1. Open `contact.md`.
2. Use the `Enter` key to create several lines of white space at the top of the file.
3. On line 1, type three hyphens: `---`.
4. On line 2, type `layout: page`.
5. On line 3, enter a page title: `title: Contact Me`. 
6. On line 4, enter in another three hyphens: `---`.
7. Save the file.
8. Run `bundle exec jekyll serve` again.
9. When you reload the page, the Contact page appears in the left sidebar and you can click on it to open the page.

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

Next we will use Jekyll front matter to perform some [Cleanup and Site and File Organization]({% link _learning-jekyll/05-learn-jekyll-organization.md %}).
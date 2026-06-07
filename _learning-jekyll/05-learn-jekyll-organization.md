---
layout: page
title: "Cleanup and Site and File Organization"
nav_order: 15
parent: "Create a Static Site Using Jekyll: Introduction"
---

# Cleanup and Site and File Organization

Your Jekyll project is in its own directory, like `learning-jekyll`, and you are tracking the project with Git. Now you need to organize the project to structure the website it will become.

1. Create a series of Markdown files and place your content. To create this tutorial, I start with an introduction: `bundle exec jekyll page "Create a Static Site Using Jekyll: Introduction"`.
2. Open each file in VS Code and paste the Markdown code for that page's content.
3. Restart the Jekyll server and see if the page shows up. You want to see the page in the sidebar and you want to be able to navigate to it and see the pages it is associated with.
4. Repeat the process, creating new Markdown pages and pasting your Markdown code into each of the pages I have set up so far. 
5. I restart the server and reload the local site.

That is a good start, but the items in the sidebar (my pages) display in alphabetical order by default, not in the order I want you to read them. That is something I will fix with front matter. I am also going to manually rename the files using digits to sort them in the order I want them, a personal preference.

```tree
├── 00-learning-jekyll-intro.md
├── 01-learning-jekyll-install-ruby-and-jekyll.md
├── 02-learning-jekyll-start-your-first-jekyll-site.md
├── 03-learning-jekyll-build-content.md
├── 04-learning-jekyll-front-matter-and-organizing.md
├── 05-learning-jekyll-cleanup-and-organization.md
```

I manually renamed the files with a two-digit sequence and prefix of how I want them to appear, but those file names are just for me. Jekyll doesn't care. Jekyll cares about the front matter.

1. Open `00-learning-jekyll-intro.md` in VS Code.
2. I'm going to add several properties to the front matter based on my previous experience. Remember, this is a basic intro to how to use Jekyll, so this is not the only way to do this or even the best way, but it's what I am doing. I add several lines of code and now my front matter for the intro page looks like this:

    ```yaml
    ---
    layout: page
    title: 'Create a Static Site Using Jekyll: Introduction'
    nav_order: 10
    has_children: true
    ---
    ```

    * `nav_order`: When you assign a `nav_order` to a series of pages, it shows how they will display in the sidebar and other navigation areas. I am going to start at 10 just because, and because this is the first page in this tutorial, it gets `10`.
    * `has_children`: I am setting `has_children` to `true` because I want to create a parent-child relationship between this page (the intro page, the parent) and all the others in the tutorial (its children).

3. I am going to go into the other pages and assign these properties to them, too. So the page you are on now has the front matter updated to this:

    ```yaml
    ---
    layout: page
    title: Cleanup and Site and File Organization
    nav_order: 15
    parent: 'Create a Static Site Using Jekyll: Introduction'
    ---
    ```

4. When I save all the pages with the new front matter, restart the server, and reload the page, they display in the order I want.

Next I will go over how to [Add Images, Links, and More to Your Jekyll Pages]({% link _learning-jekyll/06-learn-jekyll-images-and-more.md %}).

---
layout: page
title: "Integrating Learning Jekyll Into An Existing Site"
nav_order: 18
parent: "Create a Static Site Using Jekyll: Introduction"
---

# Integrating Learning Jekyll Into An Existing Site

At this stage, I have changed several things from earlier in the tutorial. Previously, I started a separate Jekyll project to demonstrate and describe the process. The intention was to describe the work from the beginning so that you, the reader, could follow along.

But I already have a Jekyll site, and that is where you are seeing this. I created that site in 2022 and the only real content was the [Security Onion tutorial]({% link _security-onion-series-macos-2022/so-00-tutorial-intro-macos-2022.md %}). But now I want to add this Jekyll tutorial to the existing website. So after I completed the previous work in this tutorial, I:

* Cloned the GitHub repository (or "repo") for my production site to my MacBook Pro.
* Created a directory, `_learning-jekyll` within that local repo, and added all the Markdown files I previously described to that directory. Here's what that directory looks like now:

    ```tree
    .
    ├── 00-learn-jekyll-intro.md
    ├── 01-learn-jekyll-installation.md
    ├── 02-learn-jekyll-start-jekyll-site.md
    ├── 03-learn-jekyll-build-content.md
    ├── 04-learn-jekyll-front-matter.md
    ├── 05-learn-jekyll-organization.md
    ├── 06-learn-jekyll-images-and-more.md
    ├── 07-building-your-jekyll-site.md
    ├── 08-automating-jekyll-build.md
    ```

* Placed these files in their own folder because, as I understand it, this is how you can create Jekyll "collections," or a series of related pages. To create a Jekyll Collection:
  * Create a sub-directory for the collection and put all of the Markdown files for that collection and the related images in that folder.

    {: .note }
    When you create a folder for your collection, the name of that folder **must** begin with an underscore (a folder name like `_learning-jekyll`) or Jekyll will not recognize it when running the build command.

  * Update the `_config.yml` file for the Jekyll site to declare the Collections. At the time of writing, mine looks like this:

    ```yaml
    # Collections
    collections:
      security-onion-series:
        output: true
        permalink: /tutorials/security-onion-series/:name/
      learning-jekyll:
        output: true
        permalink: /tutorials/learning-jekyll/:name/

    # Display Collections in Sidebar nav:
    just_the_docs:
      collections:
        security-onion-series:
          name: Security Onion Series
        learning-jekyll:
          name: Learning Jekyll
    ```

    * It took me a lot of troubleshooting (and, to be honest, consulting with Claude AI) to get this right. That second block of YAML (`# Display Collections in Sidebar nav`) is what tells Jekyll and the Just the Docs theme to put each collection in the left sidebar for easy navigation.

  * Update the [Jekyll Front Matter]({% link _learning-jekyll/04-learn-jekyll-front-matter.md %}) for each of the pages in the Collections.
  
    * The "first" or "parent" page looks like this:

      ```yaml
        ---
        layout: page
        title: "Create a Static Site Using Jekyll: Introduction"
        nav_order: 10
        has_children: true
        ---
      ```   

      * The nav_order is somewhat arbitrary. The important part for my "intro pages" is that I have `has_children: true`.

    * The "children" within that collection should have front matter that looks like this:

      ```yaml
        ---
        layout: page
        title: "Install Ruby and Jekyll"
        nav_order: 11
        parent: "Create a Static Site Using Jekyll: Introduction"
        ---
      ```

      * I set the nav_order sequentially; I am not sure if this is absolutely correct. The most important thing is to declare the correct `title` for `parent:`.

* I also moved my images for both collections into an image-specific folder named `assets`. I already had an `assets` folder with font files so that my site can load fonts independently of Google, and when Jekyll builds a site it creates its own `assets` folder. I decided it made more sense for my image files to be stored there. I needed to change the paths in my Markdown for both tutorials (for example, all of the Learning Jekyll images now start with `![](/assets/images/learning-jekyll-images/`), but I was able to accomplish that using Find and Replace in VS Code. 

## Other Customizations and Improvements

In the future, I may go over some other things I have learned about Jekyll from creating this website, including:

* Including Google Fonts locally in your `_site` build
* Various CSS customizations
* More detail on collections like my [Security Onion series]({% link _security-onion-series-macos-2022/so-00-tutorial-intro-macos-2022.md %})
* Jekyll project organization
* Customizing `_config.yml` and `Gemfile`
* Adding a custom footer that displays the last time the site was built or published

---
layout: page
title: "Building Your Jekyll Site"
nav_order: 17
parent: "Create a Static Site Using Jekyll: Introduction"
---

# Building Your Jekyll Site

The preceding pages cover my introduction to how you create and organize content for a Jekyll site. Now I will show you how to convert your Markdown pages and accompanying images into a static HTML website.

## Git Cleanup

Again, this tutorial is a very basic introduction to Jekyll and some of the other tools you use to work with Jekyll, including Git. In [Start Your First Jekyll Site]({% link _learning-jekyll/02-learn-jekyll-start-jekyll-site.md %}) I showed you some basic Git commands for tracking and committing Git files to your Git repo. Let's revisit those commands.

If you have been following the sequence of this tutorial, you have created and edited several files in your Jekyll project folder since the last time you performed a Git commit. For the purposes of demonstration, let's repeat those steps.

1. From any location within your Jekyll project, run the `git status` command. This is the output that command returns for me:

    ```bash
    $ git status
    On branch master
    Changes not staged for commit:
    (use "git add <file>..." to update what will be committed)
    (use "git restore <file>..." to discard changes in working directory)
        modified:   Gemfile
        modified:   Gemfile.lock
        modified:   _config.yml
        modified:   about.markdown

    Untracked files:
    (use "git add <file>..." to include in what will be committed)
        00-learn-jekyll-intro.md
        01-learn-jekyll-installation.md
        02-learn-jekyll-start-jekyll-site.md
        03-learn-jekyll-build-content.md
        04-learn-jekyll-front-matter.md
        05-learn-jekyll-organization.md
        06-learn-jekyll-images-and-more.md
        07-building-your-jekyll-site.md
        _posts/2026-05-10-autocreate-a-post-with-jekyll-post.md
        _posts/2026-05-10-test-post.md
        _sass/
        contact.md
        learning-jekyll-images/
        sample-page.md

    no changes added to commit (use "git add" and/or "git commit -a")
    ```

2. To stage the existing files and to "add" the newer files so that they can be tracked within the Git repo, enter `git add .`
3. When you run `git status` again, you will see something like this:

    ```bash
    $ git status
    On branch master
    Changes to be committed:
    (use "git restore --staged <file>..." to unstage)
        new file:   00-learn-jekyll-intro.md
        new file:   01-learn-jekyll-installation.md
        new file:   02-learn-jekyll-start-jekyll-site.md
        new file:   03-learn-jekyll-build-content.md
        new file:   04-learn-jekyll-front-matter.md
        new file:   05-learn-jekyll-organization.md
        new file:   06-learn-jekyll-images-and-more.md
        new file:   07-building-your-jekyll-site.md
        modified:   Gemfile
        modified:   Gemfile.lock
        modified:   _config.yml
        new file:   _posts/2026-05-10-autocreate-a-post-with-jekyll-post.md
        new file:   _posts/2026-05-10-test-post.md
        new file:   _sass/.DS_Store
        new file:   _sass/custom/custom.scss
        modified:   about.markdown
        new file:   contact.md
        new file:   learning-jekyll-images/02-learn-jekyll-start-jekyll-site-001.png
        new file:   learning-jekyll-images/06-learn-jekyll-images-and-more-001.png
        new file:   learning-jekyll-images/06-learn-jekyll-images-and-more-002.png
        new file:   learning-jekyll-images/06-learn-jekyll-images-and-more-003.png
        new file:   learning-jekyll-images/06-learn-jekyll-images-and-more-004.png
        new file:   learning-jekyll-images/06-learn-jekyll-images-and-more-005.png
        new file:   sample-page.md
    ```

4. Now I will commit those changes with `git commit -m "Final commit before demonstrating a Jekyll build"`.
5. The output looks like:

    ```bash
    $ git commit -m "Final commit before demonstrating a Jekyll build"
    [master eceb503] Final commit before demonstrating a Jekyll build
    24 files changed, 696 insertions(+), 44 deletions(-)
    ```

    * You will also see `create mode 100644` for each of the individual files that were committed. 

6. If you are working with a remote code repo like GitHub or BitBucket---which we will do later---you could push your updated local repo with a `git push` command.

## Building a Jekyll Site

When you are ready to publish your Jekyll site, you can use a single command to generate a collection of files that you can put on a web server. 

From anywhere within your Jekyll project, enter the command `bundle exec jekyll build`.

As with when you run `bundle exec jekyll serve`, you will see a lot of warnings, usually just deprecation messages that are not very helpful (especially if your Jekyll project is working as intended.)

When the build process is complete, the root folder of your Jekyll project will now contain a `_site` folder. This is your website, in a folder that you can place on a web server (for example, the `/var/www/html` on an Apache server or `/usr/share/nginx/html` for an Nginx server). This folder contains the completed HTML files that were created from the Markdown, any images or other files that will be referenced within the HTML, including an `assets` folder which contains folders for `css` (including any custom CSS you created with SASS) and `js` or JavaScript files that add functionality to your Jekyll theme or a search bar or similar, as well as any `fonts` or `images` you include.

If you want to diagram the contents of `_site`, navigate to the directory and use the `tree` command.

```bash
➜  _site git:(master) ✗ tree
.
├── 00-learn-jekyll-intro.html
├── 01-learn-jekyll-installation.html
├── 02-learn-jekyll-start-jekyll-site.html
├── 03-learn-jekyll-build-content.html
├── 04-learn-jekyll-front-matter.html
├── 05-learn-jekyll-organization.html
├── 06-learn-jekyll-images-and-more.html
├── 07-building-your-jekyll-site.html
├── 2026
│   └── 05
│       └── 10
│           ├── autocreate-a-post-with-jekyll-post.html
│           └── test-post.html
├── 404.html
├── about
│   └── index.html
├── assets
│   ├── css
│   │   ├── just-the-docs-dark.css
│   │   ├── just-the-docs-dark.css.map
│   │   ├── just-the-docs-default.css
│   │   ├── just-the-docs-default.css.map
│   │   ├── just-the-docs-head-nav.css
│   │   ├── just-the-docs-light.css
│   │   └── just-the-docs-light.css.map
│   └── js
│       ├── just-the-docs.js
│       ├── search-data.json
│       └── vendor
│           └── lunr.min.js
├── contact.html
├── feed.xml
├── index.html
├── jekyll
│   └── update
│       └── 2026
│           └── 05
│               └── 10
│                   └── welcome-to-jekyll.html
├── learning-jekyll-images
│   ├── 02-learn-jekyll-start-jekyll-site-001.png
│   ├── 06-learn-jekyll-images-and-more-001.png
│   ├── 06-learn-jekyll-images-and-more-002.png
│   ├── 06-learn-jekyll-images-and-more-003.png
│   ├── 06-learn-jekyll-images-and-more-004.png
│   └── 06-learn-jekyll-images-and-more-005.png
├── robots.txt
├── sample-page.html
└── sitemap.xml

15 directories, 35 files
```

**Note:**

* The `_site` folder is generated every time you run `bundle exec jekyll serve`, but the `bundle exec jekyll build` command is what you should run if you want to manually generate your static site.
* However, if you are troubleshooting an issue, or want a fresh start, purge the `_site` directory with the `bundle exec jekyll clean` command.

Next we are going to go beyond a website that you generate manually with the `build` command and embrace the "Docs as Code" approach and CI/CD concepts by automating the build and deployment of your website using GitHub and Amazon Web Services infrastructure and tools.
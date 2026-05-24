---
layout: page
title: "Create a Static Site Using Jekyll: Introduction"
slug: learning-jekyll-intro
nav_order: 10
has_children: true
---

# Create a Static Site Using Jekyll: Introduction

This website was created using Jekyll, a popular static-site generator. With Jekyll, you can compose your own web pages using Markdown, and Jekyll will then build those Markdown files into a static site consisting solely of HTML pages, CSS files, any image files your site uses, and a few other items.

Static sites have several advantages for simple websites, such as fast load times and inherent security since there is no database or web application functionality for threat actors to attack.

Jekyll is often used for "Docs as Code" websites. Docs as Code ["refers to a philosophy that you should be writing documentation with the same tools as code"](https://www.writethedocs.org/guide/docs-as-code/){:target="_blank"}. These websites are often integrated into the wider software applications they support [using continuous integration and continuous delivery (CI/CD)](https://www.redhat.com/en/topics/devops/what-is-ci-cd){:target="_blank"}.

In this tutorial, I'm going to provide some instructions on how to get started using Jekyll to create and build a website locally. Then we'll take that to the cloud by building our own CI/CD pipeline using AWS.

This tutorial is not exhaustive. I'm going to show you how to install Jekyll, create some content in your code editor using Markdown and some screenshots, and then preview and build that site locally. From there I'll show you how I set up the CI/CD pipeline that allows me to push code from my laptop to cloud hosts around the world.

**Note:** I use angle brackets (that is `<` and `>`) to enclose placeholder text for filenames, paths, URLs, software versions, or anything where the value may be different for you than it is for me.

## Prerequisites

This tutorial assumes an intermediate level of knowledge, skill, and familiarity. It requires you to have some familiarity with and knowledge of how the web and websites work, a solid foundation using a Unix or Linux command line, and using various services from Amazon Web Services.

I created my Jekyll site using:

* A computer: I created this tutorial using both a 2016 MacBook Pro running macOS 12 (Monterey) and later with a 2024 MacBook Pro M4 Max running macOS 26.
* A code editor: I am using Visual Studio Code ("VS Code").
* A web browser. (Or, better yet, multiple web browsers to see how your site displays and functions across those web browsers.) I use Firefox.
* A command-line terminal: I use [ITerm2](https://iterm2.com/){:target="_blank"} with Zsh for the terminal on my MacBook Pro. You could also just use the Terminal application that comes with macOS (find it under **Applications > Utilities**).
  * Zsh is command-line shell that is an alternative to Bash and is the default command-line shell in macOS since 2019. I also use ["Oh My Zsh"](https://ohmyz.sh/) to enhance Zsh functionality, which is something you can install via GitHub.
* Git: I'm using the [Git](https://git-scm.com/) version control system installed locally to work on the code. I also push this code to an online repository such as GitHub or AWS CodePipeline. This tutorial assumes you have some basic Git skills.
* I also use [Homebrew](https://brew.sh/), "The Missing Package Manager for macOS (or Linux)." I'm assuming you know how to configure and use Homebrew (or "Brew"). I used it to instal Git, the Ruby programming language that Jekyll runs on, and some other packages that make all of this possible.
* Amazon Web Services (AWS): I use various services to build and host this website.

## References

My primary source for learning about Jekyll was the [Learning Static Site Building with Jekyll course on LinkedIn Learning](https://www.linkedin.com/learning/learning-static-site-building-with-jekyll/){:target="_blank"} by [Nate Barbettini](https://www.linkedin.com/in/nbarbettini/){:target="_blank"}. This tutorial is heavily influenced by and indebted to his LinkedIn Learning course, although my deployment pipeline differs significantly. I didn't like too many of the Jekyll tutorials I found online, particularly the video ones.

You can learn more about [Markdown](https://daringfireball.net/projects/markdown/){:target="_blank"} and its [syntax](https://daringfireball.net/projects/markdown/syntax){:target="_blank"} on the website of its creator, John Gruber.

## Tutorial Items

1. [Create a Static Site Using Jekyll: Introduction]({% link learning-jekyll/00-learn-jekyll-intro.md %})
2. [Install Ruby and Jekyll]({% link learning-jekyll/01-learn-jekyll-installation.md %})
3. [Start Your First Jekyll Site]({% link learning-jekyll/02-learn-jekyll-start-jekyll-site.md %})
4. [Build Content for Your First Jekyll Site]({% link learning-jekyll/03-learn-jekyll-build-content.md %})
5. [Jekyll Front Matter]({% link learning-jekyll/04-learn-jekyll-front-matter.md %})
6. [Cleanup and Site and File Organization]({% link learning-jekyll/05-learn-jekyll-organization.md %})
7. [Add Images, Links, amd More to Your Jekyll Pages]({% link learning-jekyll/06-learn-jekyll-images-and-more.md %})
8. [Building Your Jekyll Site]({% link learning-jekyll/07-building-your-jekyll-site.md %})

To get started, [Install Ruby and Jekyll]({% link learning-jekyll/01-learn-jekyll-installation.md %}).
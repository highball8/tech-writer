---
layout: page
title: "Create a Static Site Using Jekyll: Introduction"
nav_order: 10
has_children: true
---

# Create a Static Site Using Jekyll: Introduction

This website was created using Jekyll, a popular static-site generator. With Jekyll, you can compose your own web pages using Markdown and Jekyll will then build those Markdown files into a static site consisting solely of HTML pages, CSS files, any image files your site uses, and a few other items, like some simple JavaScript for searching the site.

Static sites have several advantages for simple websites, such as fast load times and fewer security vulnerabilities since they have no database or web application functionality for threat actors to attack.

Jekyll is often used for "Docs as Code" websites. Docs as Code ["refers to a philosophy that you should be writing documentation with the same tools as code."](https://www.writethedocs.org/guide/docs-as-code/){:target="_blank"} These websites are often integrated into the wider software applications they support [using continuous integration and continuous delivery (CI/CD)](https://www.redhat.com/en/topics/devops/what-is-ci-cd){:target="_blank"}.

In this tutorial, I'm going to provide some instructions on how to get started using Jekyll to create and build a website locally. Then we'll take that to the cloud by building our own CI/CD pipeline using AWS.

This tutorial is not exhaustive. I'm going to show you how to install Jekyll, start using its commands, create some text and screenshot content in your code editor using Markdown, and then preview and build that site locally. From there I'll show you how I set up the CI/CD pipeline that allows me to push code from my laptop to the AWS cloud where it is served globally by their content distribution network.

{: .note }
**Note:** I use angle brackets (`<` and `>`) to enclose placeholder text for filenames, paths, URLs, software versions, or anything where the value may be different for you than it is for me.

## Prerequisites

This tutorial assumes an intermediate level of knowledge, skill, and familiarity. It requires you to have some familiarity with and knowledge of how the web and websites work, a solid foundation using a Unix or Linux command line, and understanding how to use various services from Amazon Web Services.

I created my Jekyll site using:

* **A computer:** I created this tutorial using both a 2016 MacBook Pro running macOS 12 (Monterey) and later with a 2024 MacBook Pro M4 Max running macOS 26.
* **A code editor:** I am using [Visual Studio Code ("VS Code")](https://code.visualstudio.com/){:target="_blank"}.
* **A web browser.** (Or, better yet, multiple web browsers to see how your site displays and functions across those web browsers.) I use [Firefox](https://www.firefox.com/){:target="_blank"}.
* **A terminal:** I use [ITerm2](https://iterm2.com/){:target="_blank"} with Zsh for the terminal on my MacBook Pro. You could also just use the Terminal application that comes with macOS (find it under **Applications > Utilities**). A "terminal" is a command-line interface---typing commands like it is the first computer you ever saw back in the day, no pointing and clicking.
  * **A shell** is the program that the terminal runs that gives you that command-line interface. The Zsh shell is an alternative to Bash and is the default command-line shell in macOS since 2019. I also use ["Oh My Zsh"](https://ohmyz.sh/) to enhance Zsh functionality, which is something you can install via GitHub.
* **[Git](https://git-scm.com/){:target="_blank"}:** Is a version control system installed locally to work on the code. I can push this code to an online repository such as GitHub or AWS CodePipeline. This tutorial assumes you have some basic Git skills.
* **[GitHub](https://github.com/){:target="_blank"}:**  is an online version of Git where you can push (upload), pull (download), and work on your code, whether it is an enterprise-scale application, Docs as Code, a static website, or even just text. It's widely used for collaboration and release management, because it creates an auditable trail of the history of the code used in an application, and a place for people to work on that code with one another.
* **[Homebrew](https://brew.sh/){:target="_blank"}** is "The Missing Package Manager for macOS (or Linux)." I'm assuming you know how to configure and use Homebrew (or "Brew"). I used it to install Git, the Ruby programming language that Jekyll runs on, Jekyll, and some other packages and dependencies that make this project possible.
* **[Amazon Web Services (AWS)](https://aws.amazon.com/){:target="_blank"}:** I use various services from AWS to build and host this website.

## References

My primary source for learning about Jekyll was the [Learning Static Site Building with Jekyll course on LinkedIn Learning](https://www.linkedin.com/learning/learning-static-site-building-with-jekyll/){:target="_blank"} by [Nate Barbettini](https://www.linkedin.com/in/nbarbettini/){:target="_blank"}. This tutorial is heavily influenced by and indebted to his LinkedIn Learning course, although my deployment pipeline differs significantly. Also, LinkedIn has made it hard to find this tutorial and they don't have that much on Jekyll in general. I didn't like too many of the Jekyll tutorials I found online, particularly the video ones. So if you're reading this, you're stuck with me for now.

You can learn more about [Markdown](https://daringfireball.net/projects/markdown/){:target="_blank"} and its [syntax](https://daringfireball.net/projects/markdown/syntax){:target="_blank"} on the website of its creator, John Gruber.

To get started, [Install Ruby and Jekyll]({% link _learning-jekyll/01-learn-jekyll-installation.md %}).
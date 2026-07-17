---
layout: page
title: "Add Images, Links, and More to Your Jekyll Pages"
nav_order: 16
parent: "Create a Static Site Using Jekyll: Introduction"
---

# Add Images, Links, and More to Your Jekyll Pages
{: .no_toc }

## Overview
{: .no_toc }

This is not an in-depth course on Jekyll. This site you are looking at represents the entirety of my Jekyll experience, so in the spirit of keeping it basic, I'm only going to cover what I needed to create what you are looking at.

1. TOC
{:toc}

## Adding Images to Your Jekyll Posts and Pages

I am an avid hobbyist photographer. I had a lot of affinity for doing things in Adobe Photoshop and in the last several years I have become a big fan of Adobe Lightroom Classic. So when I first used Snagit in 2013, I was not impressed. I was wrong. I do technical writing for a living. I like to joke that screenshots are the "bread and circuses of tech writing." And I suspect that some people have told me that they love my documentation but have probably never read it, and instead just like the presentation and the screenshots. Snagit helps me accomplish that. 

For this website and other technical writing content, I capture the screenshot with Snagit, open it in Snagit Editor, size it, add a 1px black border, and I use callouts like the red outline with a width of 5px or 6px and some border radius in the corners. Once I have captured and edited my images in Snagit, I save them with a common file format, usually portable network graphics (PNG), and usually with an incrementing digit in the filename. I save or place them in their own folder. If a single Jekyll page has a lot of screenshots, I might put all of them in their own sub-folder within the images folder.

To place the image in the post or page using Markdown, you use the following syntax, which starts with an exclamation point, then the alt text in square brackets, then the relative path to the image file (which can be a directory path or a URL) in parentheses.<br>
`![This is the alt text field](./path-to-directory/image-file-name.png)`

For this tutorial, I am going to create an image directory in the `learning-jekyll` directory and call it `learning-jekyll-images`.

So let's start with a screenshot I took earlier for the [Start Your First Jekyll Site]({% link _learning-jekyll/02-learn-jekyll-start-jekyll-site.md %}) part of this tutorial. After I started the Jekyll server, I took a screenshot to show how the site should preview. I edited the image and saved it in the `learning-jekyll-images` directory as a PNG file with a name that tells me something about it, and an incrementing digit at the end:<br>
`02-learn-jekyll-start-jekyll-site-001.png`.

I methodically name and organize my images because it allows me to insert a bunch of images into a page quickly. I can copy the image code and paste it wherever I need, as many times as I need, and then just update the digits in the file name. I recommend this approach, especially for more complex content with many images.

Now the image is created, I will place it back on that other page, after step 11.

```markdown
11. In your browser, reload the page that you last used to view the website. You will see that the new theme has been implemented and your site has a new look.
![](/assets/images/learning-jekyll-images/02-learn-jekyll-start-jekyll-site-001.png)
```

Now if you run `bundle exec jekyll serve` and load the local site, you the image displays on the page.
![](/assets/images/learning-jekyll-images/06-learn-jekyll-images-and-more-001.png)

### Decisions Around Alt Text

Adding alternative or "alt" text to your images is important for accessibility issues. It is considerate towards users who have vision issues or who use screen readers. Depending on your audience and why you are writing, it might even be required by statutes like the Americans with Disabilities Act (ADA). It can also help search engines find your content. 

However, in my technical writing, I am usually describing everything that is in a screenshot in my body text. The image itself is more decorative (going back to the "bread and circuses of tech writing" comment.) Therefore, most of the images on this site do not have alt text, because everything I would put in there is already in the body text. I believe this is consistent with the guidance from my most-trusted technical writing style guide, the [Google Developer Documentation Style Guide](https://developers.google.com/style){:target="_blank"}, which says ["If the image is purely decorative, use empty alt text... Don't present new information in images. Always provide an equivalent text explanation with the image."](https://developers.google.com/style/accessibility){:target="_blank"}

## Hyperlinks in Jekyll

Markdown already has a syntax for easily creating hyperlinks. In this section I am going to introduce some of the Jekyll-specific features you need to link your Jekyll pages together.

### A Word About Liquid

We call Jekyll a static-site generator, and it is, but you want some dynamic features within that website to make it usable. Jekyll uses the [Liquid templating language (created by Shopify)](https://shopify.github.io/liquid/){:target="_blank"} to take your static Markdown code and turn into web pages at build time. Jekyll uses Liquid to create certain elements, like {% raw %}`{% link}`{% endraw %} to process dynamic hyperlinks.

If you are writing a tutorial like this one, and you want to show all of the code syntax, format it properly in Markdown, and not cause an error in Jekyll, you need to add another code element to "escape" that code in Liquid. Whether that is inline or in a code block, you open a curly brace (`{`), a space, a percent sign (`%`), the word `raw`, then close that with a space, percent sign, and a close curly brace (`}`). When you are done with your sample that includes Liquid tags, close it again using the same tag, only with the word `endraw`. It's very hard to demonstrate this in the code itself, so I need to use a screenshot. 
![This screenshot shows how you can comment out Liquid tags within your Markdown code; the method is described in the paragraph immediately preceding this image.](/assets/images/learning-jekyll-images/06-learn-jekyll-images-and-more-002.png)

{: .note }
If you do not properly escape any and all Liquid tags, you will break your website. Which is what happened to me when I wrote this section on hyperlinks and I kept getting errors when I tried to run Jekyll serve.

### Basic Linking in Jekyll

Adding hyperlinks in your Markdown files is almost the same as adding images. Here is a code sample from the intro page that opens this tutorial:

```markdown
Jekyll is often used for "Docs as Code" websites. Docs as Code ["refers to a philosophy that you should be writing documentation with the same tools as code"](https://www.writethedocs.org/guide/docs-as-code/){:target="_blank"}. These websites are often integrated into the wider software applications they support [using continuous integration and continuous delivery (CI/CD)](https://www.redhat.com/en/topics/devops/what-is-ci-cd){:target="_blank"}.
```

This sample includes two hyperlinks to external sites, where the link text is enclosed in square brackets (`[]`), and the URL being linked to is in parentheses (`()`).

Those two links are for *external* websites. If you want to link to other *pages within your Jekyll site*, you must use a more Jekyll-specific syntax. To link back to the intro page that starts this tutorial, I refer to the page title that I declared in the Jekyll front matter (or really any other text) in square brackets, and then a relative path to the markdown file in parentheses. The Jekyll specific thing is that after you open the parentheses, you include the code {% raw %}`{% link`{% endraw %} and you close with {% raw %}`%}`{% endraw %}. So my link to [Create a Static Site Using Jekyll: Introduction]({% link _learning-jekyll/00-learn-jekyll-intro.md %}) is encoded as `{% raw %}[Create a Static Site Using Jekyll: Introduction]({% link learning-jekyll/00-learn-jekyll-intro.md %}){% endraw %}`.

### Setting the Hyperlink Target with Liquid 

Another piece of Liquid markdown that I use when creating my hyperlinks is {% raw %}`{:target="_blank"}`{% endraw %}. You use this to set the target for the hyperlink. When I want my hyperlinks to open in a new browser window or tab, I use {% raw %}`{:target="_blank"}`{% endraw %}. When Jekyll builds the site, it adds the `target="_blank"` within the `<a href="<hyperlink-URL>">` open tag for that hyperlink.

## Use SASS to Apply Custom CSS to Your Jekyll Site

Jekyll uses Syntactically Awesome Style Sheets, or SASS, as a way to apply Cascading Style Sheets (CSS) customizations to your Jekyll sites in a more programmatic way, such as declaring variables. You can use Jekyll's SASS capabilities to add custom CSS to your theme and website by creating your own SASS file within the website.

1. In the root directory of your Jekyll project, create a folder called `_sass`. You can do this through the operating system's graphical user interface (GUI), using the Explorer panel in VS Code, or on the command line with `mkdir -p _sass`.
2. Create another directory within `_sass` called `custom`. This seems unnecessary, but I think it is specific to at least the Just the Docs theme, which looks in this location for your custom SASS file (`mkdir -p _sass/custom`).
3. Navigate into this directory and create a SASS file. The name does not matter, but I think it is standard to call it `custom.scss`, where `scss` is the extension for SASS files using the newer "Sassy CSS" syntax. Again, use the GUI, VS Code, or the command line (`touch _sass/custom/custom.scss`).
4. Now that you have the `custom.scss` file, you need to tell Jekyll about it in your `_config.yml` file. Open the config file and add this code at the bottom of the file and then save `_config.yml`.

    ```yaml
    # Custom SASS/CSS
    sass:
        sass_dir: _sass
        style: compressed
    ```

5. `/_sass/custom/custom.scss` is where you will put your own CSS styles to override the theme defaults. This is not a tutorial on SASS or CSS, so I am only demonstrating customization. A problem that I want to solve is that I notice that when I create code blocks in Markdown, the text enclosed in that code block cuts off after about 100 characters, like here (notice the scroll bar under the code block):
![](/assets/images/learning-jekyll-images/06-learn-jekyll-images-and-more-003.png)
6. If I use the browser's developer tools to inspect this element, I can see that the CSS generated by Jekyll creates a CSS `code` section within a `pre` section. 
![](/assets/images/learning-jekyll-images/06-learn-jekyll-images-and-more-004.png)
7. I use some CSS knowledge to add this to `custom.scss`:

    ```css
    pre, code {
        white-space: pre-wrap;
        word-break: break-word;
    }
    ```

8. If I save `custom.scss`, restart the Jekyll server process, and reload the page, the CSS now wraps the words in my code block. (You can also see the scroll bar on the bottom of the code block no longer displays.)
![](/assets/images/learning-jekyll-images/06-learn-jekyll-images-and-more-005.png) 

## Use Plugins to Add Functionality to Your Jekyll Website

You can use Jekyll plugins to add more functionality to your Jekyll site. I am currently using four Jekyll plugins on this website:

* **[jekyll-compose](https://github.com/jekyll/jekyll-compose){:target="_blank"}:** We installed this earlier in [Build Content for Your First Jekyll Site]({% link _learning-jekyll/03-learn-jekyll-build-content.md %}). This plugin allows you to quickly create posts and pages from the command line.
* **[jekyll-feed](https://github.com/jekyll/jekyll-feed){:target="_blank"}:** This creates "an Atom (RSS-like) feed of your Jekyll posts" if you want to share or syndicate content.
* **[jekyll-sitemap](https://github.com/jekyll/jekyll-sitemap){:target="_blank"}:** This plugin helps with search engine optimization. It generates an XML sitemap and `robots.txt` file that points to the sitemap.
* **[jekyll-seo-tag](https://github.com/jekyll/jekyll-seo-tag){:target="_blank"}:** This plugin allows you to add additional metadata to your website for search engine optimization.

To add plugins to your site:

1. Go to the `Gemfile` for your Jekyll project. 
2. Previously we added `gem "jekyll-compose", group: [:jekyll_plugins]` under `# Installing Plugins`.
3. Underneath this line, add the other plugins. When you are done, it will look like this:

    ```yaml
    # If you have any plugins, put them here!
    group :jekyll_plugins do
      gem "jekyll-compose"
      gem "jekyll-feed"
      gem "jekyll-sitemap"
      gem "jekyll-seo-tag"
    end
    ```

4. Save the `Gemfile`.
5. Open `_config.yml` and look for the section `# Build settings`, where you changed the theme. Paste this block under the line where you declared the theme.

    ```yaml
    plugins:
      - jekyll-feed
      - jekyll-sitemap
      - jekyll-seo-tag
    ```

6. Save `_config.yml`.
7. Go to the command line and run the `bundle` command.

## Add Google Analytics to Your Jekyll Site

If you have a Google Analytics account, you can create a "property" and add it to your Jekyll site so that you can track traffic to the site.

1. Open the `_config.yml` file.
2. I added two lines to the bottom of my `_config.yml` file:

    ```yaml
    ga_tracking: G-01234ABCDE # Your Google Analytics 4 Measurement ID
    ga_tracking_anonymize_ip: true # To specify a GDPR compliant Google Analytics setting (true/nil by default)
    ```

3. Save `_config.yml`.

After your site is live, remember to check your Google Analytics console to see if your site is getting traffic.

Now let's move on to [Building Your Jekyll Site]({% link _learning-jekyll/07-building-your-jekyll-site.md %}).
---
layout: page
title: "Build Content for Your First Jekyll Site"
nav_order: 13
parent: "Create a Static Site Using Jekyll: Introduction"
---

# Build Content for Your First Jekyll Site

## Creating Pages and Posts

If you are familiar with WordPress or other blogging tools, you may be familiar with the concepts of a website that has "pages" and "posts." Pages are more foundational or static pieces of content that do not change often pieces of content that don't change often, like an organization's About page or Contact page (or even its Privacy Policy). Posts--like blog posts--are more temporal pieces that represent the content you are presenting to your audience, and which may have chronological or taxonomical relationships with each other. (Although I think of my own site here as entirely pages.)

### Create a Page

Your site comes with a few pages already created, including an About page (about.markdown) and `index.markdown` which acts as an `index.html` page for your website and which you can customize. 

If you wanted to create another page-type piece of content, such as a resume or a contact page, create a file in the `learning-jekyll` directory and name it `contact.md`. For demonstration purposes, it will be a very basic contact (and misleading) contact page.

1. Type `touch contact.md` and press `Enter` or click the **New file** icon in VS Code and enter `contact.md` as the file name.
2. Open `contact.md` and paste this into it:

  ```markdown
  # Contact Me

  You can email me at [email@email.com](mailto:email@email.com).

  I promise I will receive the email and get back to you.
  ```

3. Save `contact.md`

Pages can live in Jekyll site's root folder, or you can group pages in their own directories, which is something I do for this site, including this series of pages that make up my Jekyll tutorial.

While we are working on pages, if you open the `about.markdown` file that is automatically created with your Jekyll project, you will see it is prepopulated with some links to Jekyll resources. If you look at the file's contents, you will see that the first five lines of the file look like this:

```
---
layout: page
title: About
permalink: /about/
---
```

This is known as front matter and it is an essential part of Jekyll content that I will go into more detail about in the next item. 

Below line 5, I deleted what Jekyll already had and added my own text. Here is what the file looks like now:

```markdown
---
layout: page
title: About
permalink: /about/
---

This is my sample About page for my tutorial series on Jekyll. Check back for exciting new About content.
```

### Create a Post

If your file browser or the VS Code **Explorer** pane, click on the `_posts` directory within your `learning-jekyll` directory. You will see that it already has a file named `<YYYY>-<MM>-<DD>-welcome-to-jekyll.markdown`. In my case that's `2024-07-21-welcome-to-jekyll.markdown`. If you open the file in your text editor, you will see that it has instructional information about how posts must be named, always beginning with the year-month-day string, the name you would like for the post (which will also become the "slug," or name of the post its published URL), and the extension for the file type, which in this case is Markdown, or `.md` (though Jekyll uses `.markdown` as its Markdown extension). I separate the parts of my filename with hyphens; Jekyll does the same. The instructions also tell you note the front matter and Jekyll's native code highlighting abilities, which reminded me to check that out.

To create a blog post, create a new file in the `_posts` directory. Give it the appropriate date using a four-digit number for the year and two digits each for the month and day, `-test-post` and end it with the `.md` extension. I named mine `2026-05-10-test-post.md`.

### Create a Jekyll Post: Shortcut

In his [LinkedIn Learning course](https://www.linkedin.com/learning/learning-static-site-building-with-jekyll/) that is the basis for my own tutorial, Nate Barbettini shows a trick that will get you around having to create your own file by installing a Jekyll plugin.

1. Open your project's `Gemfile`.
2. Look for the line `# If you have any plugins, put them here!`. For me it was on line 18.
3. On the next line, type: `gem "jekyll-compose", group: [:jekyll_plugins]`.
4. Save the `Gemfile`.
5. Return to the command line and use the command `bundle`, which will install the Gem.
6. Now you can create your new blog post file from the command line. From within your Jekyll project directory, type `bundle exec jekyll post` and follow that with the post title you want in double quotes: `bundle exec jekyll post "Autocreate a Post with Jekyll Post"`.
7. The command should generate command-line output that looks like this:

    ```bash
    Configuration file: /Users/tech-writer/Desktop/learning-jekyll/_config.yml
    New post created at _posts/2026-05-10-autocreate-a-post-with-jekyll-post.md
    ```

8. Look in the `_posts` directory and your new post should be there. In my case, the filename was `2026-05-10-autocreate-a-post-with-jekyll-post.md`.
9. If you open the file, you will see the basic Jekyll front matter has been prepopulated:

    ```yaml
    --- 
    layout: post
    title: Autocreate a Post with Jekyll Post
    date: 2026-05-10 18:39 -0400
    ---
    ```

10. Now you have a blank post to create content in.

The `jekyll` command also works with pages. If I want to create a page with it, I could type `bundle exec jekyll page "Sample Page"`. If you look in your present working directory you will see a `sample-page.md` and if you open it you can see it has been prepopulated with Jekyll front matter.

```yaml
---
layout: page
title: Sample Page
---
```

Now we definitely need to talk about [Jekyll Front Matter]({% link learning-jekyll/04-learn-jekyll-front-matter.md %}).

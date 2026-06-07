---
layout: page
title: "Install Ruby and Jekyll"
nav_order: 11
parent: "Create a Static Site Using Jekyll: Introduction"
---

# Install Ruby and Jekyll

I followed [the instructions on the official Jekyll website](https://jekyllrb.com/docs/installation/macos/){:target="_blank"} to install Ruby on a macOS system using Brew.

First you need to install [Ruby, the open-source programming language](https://www.ruby-lang.org/){:target="_blank"} that Jekyll is written in. Ruby installation is pretty easy with Brew. Once you have Ruby installed, you install Jekyll as a "gem," or a Ruby package.

1. Open your terminal/command-line interface/shell, whatever you want to call it, I won't judge you.
2. Start by installing three packages: `chruby`, a version-management tool for Ruby, `ruby-install`, a utility that handles Ruby installation, as well as [XZ Utils, which is a data compression utility](https://github.com/tukaani-project/xz/blob/master/README){:target="_blank"}, and Git (assuming it is not already installed): `brew install chruby ruby-install xz git`
3. Now use Homebrew's ruby-install package to install Ruby. I am installing Ruby 4.0.3, which was the stable version when I wrote this tutorial: `ruby-install ruby 4.0.3`
4. The installation may last about two minutes and the terminal will output a lot of text, but at the end you should see `>>> Successfully installed ruby 4.0.3 into ~/.rubies/ruby-4.0.3`. (I am using `~/` as a shorthand to represent the home directory (or folder) of my user account on the MacBook Pro.)
5. You want to configure your shell to use this installation of Ruby, and not another installation (such as the Ruby installation used by your macOS operating system). Since I am using Zsh, I use these three commands, which send the commands to `~/.zshrc` which is like your Zsh instance's preferences file:

    ```bash
    echo "source $(brew --prefix)/opt/chruby/share/chruby/chruby.sh" >> ~/.zshrc
    echo "source $(brew --prefix)/opt/chruby/share/chruby/auto.sh" >> ~/.zshrc
    echo "chruby ruby-4.0.3" >> ~/.zshrc # run 'chruby' to see actual version
    ```

    * You may want to confirm that those source commands were written to `.zshrc`. You can do that with `less ~/.zshrc`, then looking at the end of the file to confirm you see the new lines appended to the file.

6. You now need to "source" Zsh with `source ~/.zshrc`. This makes sure Zsh starts using those commands you just sent to the preferences.
7. Confirm the version of Ruby you have with one or both of these commands:

    * The command `which -a ruby` should output `~/.rubies/ruby-4.0.3/bin/ruby` and may also display `/usr/bin/ruby`.
    * The command `ruby -v` should return `ruby 4.0.3 (2026-04-21 revision 85ddef263a) +PRISM [arm64-darwin25]` but will vary based on what kind of computer you have.

8. Now you can install Jekyll itself as a Ruby gem: `gem install jekyll`.
9. That command will output many lines of text, one of which should be `Successfully installed jekyll-4.4.1`. (Depending on when you do this, you may have a version later than 4.4.1.)
10. Check your installation with `which jekyll`, which should return `~/.gem/ruby/4.0.3/bin/jekyll`.
11. You can also use `jekyll -v`, which should return `jekyll 4.4.1`.

Now you're ready to [Start Your First Jekyll Site]({% link _learning-jekyll/02-learn-jekyll-start-jekyll-site.md %}).
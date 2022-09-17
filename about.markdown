---
layout: page
title: About
permalink: /about/
nav_order: 2
---

My name is Phil. I have created this website using Jekyll as a way to showcase my technical writing skills, particularly as they relate to information security and related information-technology themes. The problem with working as a technical writer is that almost everything I create for work is covered by a non-disclosure agreement (NDA), and I can't share my work product with anybody, from friends and family (not that they actually want to see it) to potential employers (honestly, most of them don't want to see it, either).

I got into this world via WordPress, which I think is great. I previously created two separate WordPress sites to showcase my technical and creative abilities.

* **[Massolit-Media.com](https://www.massolit-media.com/){:target="_blank"}:** This is a portfolio site. It's kind of out of date. The original theme, which I have never changed, is that of a (fake) creative services agency that can help you with everything from photography and content writing to videos and websites. I never ran such a business, and today "technical writing" is how I make money and stay interested in how I make money. So this site is a "spinoff"&mdash;all technical writing, all the time.
* **[Highball8.com](https://www.highball8.com/){:target="_blank"}:** I like trains and riding trains. This website was supposed to be a creative outlet and a way to showcase my "content marketing" abilities. Well, anyway, since getting into the tech side of things on one hand, and a lack of train trips on the other (thanks, COVID), I haven't updated it in a long time.

So now I am creating this website. I will use it to create information-security-specific writing samples, but it's also a way to learn lots of other things. I am foregoing WordPress for [Jekyll](https://jekyllrb.com/){:target="_blank"}, a static-site generator widely used for creating software documentation. I'm combining Jekyll with the following technologies to create a real-life "Docs as Code" website with its own Continuous Integration/Continuous Deployment (CI/CD) pipeline:

* **[Git](https://git-scm.com/) and [GitHub](https://github.com/){:target="_blank"}:** I am creating the Jekyll site locally, tracking changes in Git, and pushing those changes to a repository ("repo") on my GitHub account.
* **[Travis CI](https://app.travis-ci.com/){:target="_blank"}:** The LinkedIn Learning course that I took showed me some basic Jekyll, but also how to publish Jekyll on Amazon Web Services (AWS) with the help of a Travis CI account and script.
* **[Amazon Web Services (AWS) Simple Storage Solution (S3)](https://aws.amazon.com/s3/){:target="_blank"}:** My Travis script builds all my Jekyll site and uploads it to an S3 bucket.
* **[AWS CloudFront](https://aws.amazon.com/cloudfront/){:target="_blank"}:** I created a CloudFront distribution that publishes the S3 bucket as a CloudFront distribution, updating it every time I push changes to GitHub, and even providing a TLS/SSL certificate.
* **[AWS Route 53](https://aws.amazon.com/route53/){:target="_blank"}**: I created this subdomain (**[tech-writer.massolit-media.com](https://tech-writer.massolit-media.com/)**) using Amazon Web Services's Route 53 for DNS management. (Honestly I had a lot of problems. It was my first time setting up a subdomain.)

Like I said, the website you are looking at was created using [Jekyll](https://jekyllrb.com/){:target="_blank"}, a static-site generator built on [Ruby](https://www.ruby-lang.org){:target="_blank"}. I thought "static sites" and though it would be simple. It's very powerful. I'll tell you more when I learn more.

The theme I am using is called Just the Docs. I'm learning about it by checking out [their GitHub](https://github.com/just-the-docs/just-the-docs){:target="_blank"} and [their own documentation site](https://just-the-docs.github.io/just-the-docs/){:target="_blank"}. I've also been checking out [OpenSearch's implementation of Just the Docs on GitHub](https://github.com/opensearch-project/documentation-website){:target="_blank"} for some additional guidance.


---
weight: 3
type: docs
bookToc: false
---

<h1>thank you kind sir</h1>

**as** an open-source organization, *hotpotcookie* site offers three main contents for you to share your cool and edgy ideas of contents to the readers, which are [blog](/posts/blog), [paper](/posts/paper), and [write-up](/posts/writeup). **your** submission will take place online on our site at least within 48 hours after your ```commit``` since it requires proofreading from our internal team. **as** for the [payloads](/docs/gg/payload/) and [pentest tool](/docs/gg/pentest-tool/), it's going to be reviewed & tested first in a local lab within a whole week before merging it to the main arsenal.

## consider the following

**since** all the contributions are based on your pull request, here are some things that you need to consider for the content of your submissions to meet our baseline template: 

- **the** submission should be written in a ```.md``` format
- **what** count as a contribution are creating content, fixing bugs & typos, or adding any minor or major significant improvement
- **submitted** images should be in a ```.webp``` format, ideally less than around ```800,0 KiB``` collectively for a single post. **the** naming template for those images should be defined by the post's ```id```, such as ```[post-id]-[n].webp``` with ```[n]``` as the n-th images that you provided and stored in ```/main/static/images/data/[content]/```
- **the** usage of [asciinema](https://asciinema.org/) with [agg](https://github.com/asciinema/agg) are preferable as it gives clarity to the context of what the commands are cookin

## local repository

**once** your have forked [hotpotcookie](https://github.com/hotpotcookie/hotpotcookie) locally, the last thing you wanted to do is to submit the posts via pull requests. **for** a start, we will clone the forked repo and switch the branch from ```main``` to ```contrib```. **your** push on branch ```contrib```, later on, will be merged to the main repository for your posts to live on-site.

```markdown
$ git clone https://github.com/[username]/hotpotcookie.git
$ cd hotpotcookie/
$ git checkout -b contrib
$ git remote add upstream https://github.com/hotpotcookie/hotpotcookie.git
```

## markdown template & git staging

**as** we refer from those points before, here are some base ```.md``` template files to give you some contexts for each type of content that you might contribute to, check them out.

{{< hint warning >}}
**please** verify that each file is placed to the corressponding directory, as it will significantly minimize the work on fixing the file path before rebuilding the site. **you** can follow the commands below on handling each type of file that is going to be staged
{{< /hint >}}

{{< tabs "uniqueid" >}}
  
  {{< tab "Blog" >}}
  **a** blog is where you can post your ideas, news & articles, or projects and concepts that you've been working on while being too technical is not mandatory in this case. **there** are 3 main ```categories``` of the blog's content that are being used on this site: 

  - ***response***, simple post that is written as a form of response that focuses on providing an easy-to-understand answer
  - ***staple***, general & shareable post that provide more information on the subject, which may contain tips, a how-to guide, and well-depth responses
  - ***pillar***, post that covers all the aspects of the given topic in a detailed manner and may heavily depend on using codeblocks for snippets, which makes it the heaviest content among the three
  - **proof-of-concept**, a complementary tag for a pillar, which gives the context that your post contains any of your development that may bring some form of novelty about the topic itself

  **for** this example, you may post a content titled *"Embedding Log4Shell to BadSUB for Remote Access Trojan"*. **the** file name of your post should be the shortened form of the title, such as ```embedding-log4shell-to-badusb-for-rat.md```. **here** is a mockup template of the file for you to modify it:
  ```java {linenos=inline, linenostart=1}
  ---
  id: eltbfrat // the acryonym of your title
  linktitle: "Embedding Log4Shell to BadSUB for Remote Access Trojan" // may consist of around 6-12 words in length
  date: YYYY-MM-DD // the published or last modfied date format
  tags: ["Vulnerability Analysis", "Exploitation", "CVE-2022-44877"] // may consist of main topics, subjects, vulnerability references, etc.
  categories: ["Pillar", "Proof-of-Concept"] // consist of Response, Staple, Pillar & Proof-of-Concept
  type: posts // mandatory value for all form of content
  ---

  ##  heading-2 // level-2 heading is preferred to start the blog since the title already used h1
  ### heading-3 // it is recommended not to exceed the level-3 heading as it tends to be hard to read the table of contents
  ![cat](/images/data/blog/eltbfrat-1.webp) // (1/2) ways of importing image
  <img src="/images/data/blog/eltbfrat-2.webp" alt="cat"/> // (2/2) ways of importing image
  
  ## references // level-2  heading for reference on the last section of the post
  - [title - site](URL) // list of all the sites that you may cite or use
  - [Introduction to Log4j - **Medium***](https:..) // citation example from the format above
  ```
  **when** all the needed files are ready, including the post and the images, you can finally stage all those resources and commit it. **here** is the snippet with the relative path to the corresponding files.

  ```markdown
$ git add content/posts/blog/embedding-log4shell-to-badusb-for-rat.md
$ git add static/images/data/blog/eltbfrat-*.webp
$ git commit -m "adding my content with its image resources"
```
  {{< /tab >}}


{{< tab "Paper" >}} undergo {{< /tab >}}
{{< tab "Write-Up" >}} undergo {{< /tab >}}
{{< tab "Payload" >}} undergo {{< /tab >}}
{{< tab "Pentest Tool" >}} undergo {{< /tab >}}

{{< /tabs >}}

**as** for your contribution profile to appearing on the [about us](/docs/org/about-us/) page, you can submit your [villager](https://meiker.io/play/11374/online.html) in ```/main/static/images/profile``` with your [GitHub](https://github.com) username as the file name of it, such as ```[username].webp```. **notice** that this step is one time only, unless you wanted to change it later on.

```markdown
$ git add static/images/profile/[username].webp
$ git commit -m "adding my villager avatar"
```
## pushing your commits

**once** all the files have been staged and committed, the last thing to do is push your commits to the remote branch on the main repository. **that** way, we can review and merge it if it passes the criteria that are mandatory or needed.

```markdown
$ git push -u origin contrib
```
---
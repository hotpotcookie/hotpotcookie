---
weight: 3
type: docs
bookToc: false
---

<h1>thank you kind sir</h1>

**as** an open-source organization, *hotpotcookie* site offers 3 main different contents for you to share your cool and edgy ideas and thoughts to the readers, which are [blog](/posts/blog), [paper](/posts/paper), and [write-up](/posts/writeup). **your** submission will take place online in our site atleast within 48 hours after your commit, since it requires proofreading from our internal team. **as** for the [payloads](/docs/gg/payload/) and [pentest tool](/docs/gg/pentest-tool/), it's going to be reviewed & tested first in a local lab within a full one week before merging it to the main arsenal

## consider the following

**since** all the contributions are based on your pull request, here are some things that you need to consider as for the content of your submissions to basically meet our baseline template: 
- **the** submission should be written in a ```.md``` format
- **what** count as a contribution are creating content, fixing bug & typo, or adding any minor or major improvement
- **submitted** images should be in a ```.webp``` format that ideally less than around ```100,0 KiB``` and stored in ```/main/static/images/data/[content]/```. **the** naming template for those images should be defined by the post's ```id```, such as ```[post-id]-[n].webp``` with ```[n]``` is your n-th images that you provided
- **the** usage of [asciinema](https://asciinema.org/) are preferrable as it gives clarity to the context of what the commands are cookin

## markdown template

**as** refer from those points before, here are the base ```.md``` template file to give you some contexts for each type of contents that you might contribute to, check it out

{{< tabs "uniqueid" >}}
  
  {{< tab "Blog" >}}
  **blog** is where you can post your ideas, news & articles, or projects and concepts that you've been working on, while being too technical is not a mandatory in this case. **there** are 3 main ```categories``` of the blog's content that being used in this site: 
  - ***response***, simple post that written as a form of response to a question that focus on providing easy to understand answer. **it** is recommended to be anywhere between 1350 to 1500 words
  - ***staple***, general & shareable post that provide more information to the given subject, which my contain tips, a how-to-guide, and well-depth responses. **it** is recommended to be more than 2000 words
  - ***pillar***, cover all the aspects of the given topic in a detail manner, which make it the heaviest content amongst the three. **it** is recommended to be more than 3000 words
  - **proof-of-concept**, a complementary tags for pillar, which give the context that your post contains any of your own development that may bring some form of novelty about the topic itself

  **for** this example, you may post a content with the title of *"Embedding Log4Shell to BadSUB for Remote Access Trojan"*. **the** file name of your post should be the shortened form of the title, such as ```embedding-log4shell-to-badusb-for-rat.md```, which here is a mockup template of the file for you to modify it:
  ```java {linenos=inline, linenostart=1}
  ---
  id: eltbfrat // the acryonym of your title
  linktitle: "Embedding Log4Shell to BadSUB for Remote Access Trojan" // may consist of around 6-12 words length
  date: YYYY-MM-DD // the published or last modfied date format
  tags: ["Vulnerability Analysis", "Exploitation", "CVE-2022-44877"] // may consist of main topics, subjects, vulnerability references, etc.
  categories: ["Pillar", "Proof-of-Concept"] // consist of Response, Staple, Pillar & Proof-of-Concept
  type: posts // mandatory value for all form of content
  ---

  ##  Heading-2 // level-2 heading are preferred to start the blog, since the title already used h1
  ### Heading-3 // it is recommended to not exceed the level-3 heading at it tends to hard to read the table of contents
  ![cat](/images/data/blog/eltbfrat-1.webp) // (1/2) ways of importing image
  <img src="/images/data/blog/eltbfrat-2.webp" alt="cat"/> // (2/2) ways of importing image
  
  ### References // level-3 heading for reference on the last section of the post
  - [title - site](URL) // list of all the sites that you may cite or use
  - [Introduction to Log4j - Medium](https:..) // citation example from the format above
  ```
  {{< /tab >}}


{{< tab "Paper" >}} undergo {{< /tab >}}
{{< tab "Write-Up" >}} undergo {{< /tab >}}
{{< tab "Payload" >}} undergo {{< /tab >}}
{{< tab "Pentest Tool" >}} undergo {{< /tab >}}

{{< /tabs >}}

**as** for your contribution profile to be appeared in the [about us](/docs/org/about-us/) page, you can submit your [villager](https://meiker.io/play/11374/online.html) in ```/main/static/images/profile``` with your [GitHub](https://github.com) username as the file name of it, such as ```[username].webp```. notice that this step is one time only, unless you want to medify

## creating pull request

**once** your have forked [hotpotcookie](https://github.com/hotpotcookie/hotpotcookie) locally, the last thing you wanted to do is to submit the posts via pull requests. **for** the start, we're going to clone the forked repo and switch the branch from ```main``` to ```contrib```. **your** push on branch ```contrib``` later on will be merge to the main repository for your posts to live on-site

```markdown
$ git clone https://github.com/[username]/hotpotcookie.git
$ cd hotpotcookie/
$ git checkout -b contrib
$ git remote add upstream https://github.com/hotpotcookie/hotpotcookie.git
```

**after** your local repository and your documents is ready, make sure to verify that each file is placed with its correspond directory, which is shown [template](#markdown-template) before. here are some example on adding and committing the post document, the image resources, and your avatar profile ...

```markdown
$ ll content/posts/blog/
.rw-rw-r--  64 user 10 May 15:13 _index.md
.rw-rw-r-- 538 user 10 May 17:24 embedding-log4shell-to-badusb-for-rat.md
.rw-rw-r-- 538 user 10 May 17:24 ...

$ git add content/posts/blog/embedding-log4shell-to-badusb-for-rat.md
$ git commit -m "adding my first post"
```
```markdown
$ ll static/images/data/blog/
.rw-rw-r-- 11k user 10 May 08:22 eltbfrat-1.webp
.rw-rw-r-- 13k user 10 May 08:25 eltbfrat-2.webp
.rw-rw-r-- 538 user 10 May 17:24 ...

$ git add static/images/data/blog/eltbfrat-*.webp
$ git commit -m "adding my image resources of the post"
```
```markdown
$ ll static/images/profile/
.rw-rw-r-- 11k user 10 May 08:22 [username].webp
.rw-rw-r-- 538 user 10 May 17:24 ...

$ git add static/images/profile/[username].webp
$ git commit -m "adding my villager avatar"
```
```markdown
$ git push -u origin contrib
```
---
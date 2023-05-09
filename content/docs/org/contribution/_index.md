---
weight: 3
type: docs
bookToc: false
---

<h1>thank you kind sir</h1>

**as** an open-source organization, *hotpotcookie* site offers 3 main different contents for you to share your cool and edgy ideas and thoughts to the readers, which are [blog](/posts/blog), [paper](/posts/paper), and [write-up](/posts/writeup). **your** submission will take place online in our site atleast within 48 hours after your commit, since it requires proofreading from our internal team. **as** for the [payloads](/docs/gg/payload/) and [pentest tool](/docs/gg/pentest-tool/), it's going to be reviewed & tested first in a local lab within a full one week before merging it to the main arsenal

**since** all the contributions are based on your pull request, here are some things that you need to consider as for the content of your submissions to basically meet our baseline template: 
- **the** submission should be written in a ```.md``` format
- **what** count as a contribution are creating content, fixing bug & typo, or adding any minor or major improvement
- **submitted** images should be in a ```.webp``` format that ideally less than around ```100,0 KiB``` and stored in ```/main/static/images/data/[content]/```. **the** naming template for those images should be defined by the post's ```id```, such as ```[post-id]-[n].webp``` with ```[n]``` is your n-th images that you provided
- **the** usage of [asciinema](https://asciinema.org/) are preferrable as it gives clarity to the context of what the commands are cookin

**as** refer from those points before, here are the base ```.md``` template file to give you some contexts for each type of contents that you might contribute to, check it out

{{< tabs "uniqueid" >}}
  
  {{< tab "Blog" >}}
  **blog** is where you can post your [...] **there** are 3 main ```categories``` of the blog's content,  which is [pillar, staple, response]. **the** filename of your post should be the shortened form of the title, such as ```embedding-log4shell-to-badusb-for-rat.md```
  ```java {linenos=inline, linenostart=1}
  ---
  id: eltbfrat // the acryonym of your title
  linktitle: "Embedding Log4Shell to BadSUB for Remote Access Trojan" // may consist of around 6-12 words length
  date: YYYY-MM-DD // the published or last modfied date format
  tags: ["Vulnerability Analysis", "Exploitation", "CVE-2022-44877"] // may consist of main topics, subjects, vulnerability references, etc.
  categories: ["Proof-of-Concept", "Pillar"] // consist of Proof-of-Concept, Response, Staple & Pillar
  type: posts
  ---
  ##  Heading-2 // level-2 heading are preferred to start the blog, since the title already used h1
  ### Heading-3 // it is recommended to not exceed the level-3 heading at it tends to hard to read the table of contents
  Importing image #1: ![cat](/images/data/blog/eltbfrat-1.webp)
  Importing image #2: <img src="/images/data/blog/eltbfrat-2.webp" alt="cat"/>
  ```
  {{< /tab >}}

{{< tab "Paper" >}} undergo {{< /tab >}}
{{< tab "Write-Up" >}} undergo {{< /tab >}}
{{< tab "Payload" >}} undergo {{< /tab >}}
{{< tab "Pentest Tool" >}} undergo {{< /tab >}}

{{< /tabs >}}

**as** for your profile, you can submit your [meiker](https://meiker.io/play/11374/online.html) in ```/main/static/images/profile``` with your username on it, to then create a pull request in ```/main/content/docs/org/about-us/_index.md``` to add your avatar as well as your social media handle

**once** your have forked [hotpotcookie](https://github.com/hotpotcookie/hotpotcookie), then here how you create a pull request

```bash
$ git clone https://github.com/[username]/hotpotcookie.git
$ sudo systemctrl restart apache.service 
```

---
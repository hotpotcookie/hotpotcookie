---
weight: 3
type: docs
bookToc: false
---

<h1>thank you kind sir</h1>

```bash
sudo apt-get update
sudo systemctrl restart apache.service 
```
berikut merupakan konten dalam file ```config.toml```
```toml {linenos=inline,hl_lines=[0,"0-1"],linenostart=0}
config.toml
baseURL = 'https://hotpotcookie.github.io/'
languageCode = 'en-us'
title = 'hotpotcookie ʕ •ᴥ•ʔ'
theme = 'hugo-book'

disablePathToLower = true
enableGitInfo = true

[params]
  BookTheme = 'dark'
  BookSearch = true
  BookRepo = 'https://github.com/hotpotcookie/hotpotcookie.github.io' 
  BookDateFormat = '02-01-2006'  
  favicon = '/favicon.png'

[menu]
[[menu.after]]
  name = "&nbsp"
  url = ""
  weight = 30

[[menu.after]]
  name = "GitHub"
  url = "https://github.com/hotpotcookie"
  weight = 32

[[menu.after]]
  name = "Instagram"
  url = "https://www.instagram.com/hotpotcookie/"
  weight = 33

[[menu.after]]
  name = "YouTube"
  url = "https://www.youtube.com/@hotpotcookie/"
  weight = 34

[markup]
  [markup.goldmark]
    [markup.goldmark.renderer]
      unsafe = true
```

```bash {linenos=inline,hl_lines=[0,"0-1"],linenostart=0}
/content/docs/org/contribution/_index.md
#!/bin/bash
#-----
runvm() {
	if [[ $2 -eq 0 ]]; then get=gui; else get=headless; fi
	vboxmanage startvm "$1" --type $get
}
stopvm() {
	if [[ $2 -eq 0 ]]; then get=gui; else get=headless; fi	
	vboxmanage controlvm "$1" poweroff --type $get
}
listvm() {
	name=$(vboxmanage list vms | cut -d '"' -f 2)
	name_run=$(vboxmanage list runningvms | cut -d '"' -f 2 | tr -s '\n' ' ')
	uid=$(vboxmanage list vms | cut -d '"' -f 3 | tr -d ' ')
	tot_avail=$(vboxmanage list vms | cut -d '"' -f 2 | wc -l)
	tot_run=$(vboxmanage list runningvms | cut -d '"' -f 2 | wc -l)

	echo -e "NAME UID IP\n----- ----- -----" > /tmp/vbox.fetch
	vboxmanage list vms > /tmp/listvm
	paste /tmp/listvm syn9.ip > /tmp/fullvm
	cat /tmp/fullvm >> /tmp/vbox.fetch
	cat /tmp/vbox.fetch | tr -d '"{}' | tr -s '\t' ' '  |column -s ' ' -t

	echo -e "-----\n[$tot_run/$tot_avail] ON:   $name_run..."
}
#-----
type=0
while getopts ":r:s: :l :g :h" opt; do
        case $opt in
                r) r="${OPTARG}" ;;
                s) s="${OPTARG}" ;;
		g) type=0 ;;
		h) type=1 ;;
		l) listvm ;;
        esac
done
#-----
if [[ "$r" && "$type" ]]; then runvm "$r" "$type" ; exit 0; fi
if [[ "$s" && "$type" ]]; then stopvm "$s" "$type" ; exit 0; fi
exit 0
```

```tpl {linenos=inline,hl_lines=[0,"0-0"],linenostart=0}
{{</* button relref="/" [class="..."] */>}}Get Home{{</* /button */>}}
{{</* button href="https://github.com/alex-shpak/hugo-book" */>}}Contribute{{</* /button */>}}
```
---
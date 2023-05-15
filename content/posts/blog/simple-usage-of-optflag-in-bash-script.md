---
id: suoofibs
date: 2023-05-14
linktitle: "Simple Usage of Optional Flags in Bash Script"
tags: ["Bash", "Scripting"]
categories: ["Staple"]
type: posts
---
<img src="/images/data/blog/flower-1.webp" alt="cookie-banner" width="100%" style="border-radius: 0.5rem;"/></a>

---

## what is optional flags?
**one** of the powerful feature in command-line programs is that having the capability to passing multiple arguments on the time of the execution. **that** way, the program can straight up run the way we wanted to without having another ```STDIN``` sessions to take the user input.

**there** are multiple ways on passing multiple arguments and parsing it in such way that the program could read without hassle. **one** of the best appraoch is to having optional flags. **these** flags are either represented by character letters preceded by a hpyhen, ```-u duke64```, or by a word that preceded by double hyphen, ```--username duke64```. **the** parameteter value of each corresponding flag is defined next to it by whitespace.

**one** of the shell's built-in that designated for this feature is ```getopts``` utility, which to retrive options and option-arguments from a list of parameters. ```getopts``` itself is a replacement for GNU/Linux utility ```getopt``` as being a standalone program. **even** though both serve the same main function, one of the difference is that ```getopts``` cannot read word-based flags, while ```getopt``` can. **to** overcome that, while still maintaining the readability and the simplicty of the script from using ```getopt```, we are going to use positional arguments instead, such as ```$1```, that are being passed and parsed manually later on.

## simple use case
**there** are two cases that we are going to demonstrate, and that is the usage of ```getopts``` in ```testflag-1.sh``` and positional arguments in ```testflag-2.sh```. **both** scripts are going to contain the same mockup functions that later on going to be tested, they are:
- ```usage()``` for listing the possible flags
- ```invalid()``` for throwing erorr message of unknown flag(s)
- ```generate()``` as the non-argument flag function to generate the whole output message.

```bash {linenos=inline, linenostart=1}
#!/bin/bash
#----------
usage() {
  echo "list of available options goes here"
  exit 0; }
invalid() {
  echo "testflag: detecting improper option"
  echo "try option '-h' for more information"
  exit 1; }
generate() {
  echo "my name is $1 ($3)" | grep -E --color "$1|$3"
  echo "i am $2 years old"  | grep -E --color "$2"
  exit 0; }
#----------  
```

### getopts
getopts >> usage of optsring & name
```bash {linenos=inline, linenostart=14}
#----------
while getopts "n: a: s: :g :h" opt; do
  case $opt in
    n) n="${OPTARG}" ;;
    a) a="${OPTARG}" ;;
    s) s="${OPTARG}" ;;
    g) opt_sub="generate" ;;
    h) usage ;;
    *) invalid ;;
  esac
done
#----------
```

### positional arguments
manually
```bash {linenos=inline, linenostart=14}
#----------
args=(n name a age s sex g generate h help)
while [ $# -gt 0 ]; do
  if [[ "$1" == -* ]]; then
    raw_opt=$(printf "%s\n" "$1" | tr -d '-')
    if [[ $raw_opt ]]; then
      if [[ $(echo "${args[@]}" | grep -ow "$raw_opt" | wc -w) -eq 1 ]]; then
        case $1 in
          -n | --name)      n="$2" ;;
          -a | --age)       a="$2" ;;
          -s | --sex)       s="$2" ;;
          -g | --generate)  opt="generate" ;;
          -h | --help) usage ;;
        esac
      else
        echo "$0: illegal option -- $raw_opt"
        invalid
      fi
    fi
  fi
  shift  
done
#----------
```

## the verdict is in
undergo

## references
- [Bash Tutorial: getopts | **stackchief**](https://www.stackchief.com/tutorials/Bash%20Tutorial%3A%20getopts)
- [Using --getopts to Pick Up Whole Word Flags - Bash | **AppsLoveWorld**](https://www.appsloveworld.com/bash/100/16/using-getopts-to-pick-up-whole-word-flags)
- [How to Pass Command Line Arguments to Bash Script | **Baeldung**](https://www.baeldung.com/linux/pass-command-line-arguments-bash-script)
- [Beginners Guide to Use getopts in Bash Scripts & Examples | **GoLinuxCloud**](https://www.golinuxcloud.com/bash-getopts/#:~:text=getopt%20vs%20getopts,-getopts%20is%20a&text=The%20main%20differences%20between%20getopts,needs%20to%20be%20installed%20separately)

---
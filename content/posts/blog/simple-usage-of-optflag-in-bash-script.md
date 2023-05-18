---
id: suoofibs
date: 2023-05-14
linktitle: "Simple Usage of Optional Flags in Bash Script"
tags: ["Bash", "Scripting"]
categories: ["Staple"]
type: posts
---
<img src="/images/data/blog/suoofibs-banner.webp" alt="cookie-banner" width="100%" style="border-radius: 0.5rem; margin-top: 1rem;"/>

---

## what is optional flags?
**one** of the powerful features of command-line programs is the capability to pass multiple arguments during the time of execution. **that** way, the program can run straight-up the way we wanted to without having another ```STDIN``` session to take the user input.

**there** are multiple ways of passing multiple arguments and parsing them so the program can read them without hassle. **one** of the best approaches is to have optional flags. **these** flags are represented by character letters preceded by a hyphen, ```-u duke64```, or by a word preceded by a double hyphen, ```--username duke64```. **the** parameter value of each corresponding flag is defined next to it by whitespace.

**one** of the program that is designated for this feature is the ```getopts``` utility, which retrieves options and option arguments from a list of parameters. ```getopts``` is a replacement for GNU/Linux utility ```getopt``` from a standalone program to become a shell's built-in command. **even** though both serve the same main function, one difference is that ```getopts``` cannot read word-based flags, while ```getopt``` can. **to** overcome that while still maintaining the script's readability and simplicity from using ```getopt```, we will use positional arguments instead, such as ```$1```, that will be passed and parsed manually later on.

## simple use case
**there** are two cases that we will demonstrate: the use of ```getopts``` in ```testflag-1.sh``` and positional arguments in ```testflag-2.sh```. **both** scripts are going to contain the same mockup functions that are later on going to be tested; they are:
- ```usage()``` for listing the possible flags
- ```invalid()``` for throwing erorr message of unknown flag(s)
- ```generate()``` as the non-argument flag function to generate the whole output message, with the argument ```$1``` for the name of the user, ```$2``` for the age, and ```$3``` for the sex

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
**in** ```getopts```, a collection of the valid option letters, ```OPTSTRING```, will determine whether the flag is argument-based or not. **that** distinction is defined by the usage of a trailing semicolon ```:```, which indicates that an argument variable called ```OPTARG``` will set that particular argument from the flag. **here** are the following snippets on the overall usage of ```getopts```:

```bash {linenos=inline, linenostart=14}
#----------
while getopts "n: a: s: g h" opt; do
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
case $opt_sub in
  "generate") [[ "$n" && "$a" && "$s" ]] && generate "$n" "$a" "$s" || invalid ;;
esac
#----------
usage
```
**the** argument-based flag in ```OPTSTRING``` that is going to take the user’s arguments are ```n:``` for the name of the user, ```a:``` for the age, and ```s:``` for the sex. **as** one of the improvement from ```getopts```, it will also throws an error if an argument from the argument-based flag is not supplied, which is set to an explicit ```null```.

**each** ```OPTSTRING``` option, later on, will be iterated from the ```while``` loop and checking it to its corresponding letter via ```case``` statement. **if** the provided flag by the user does not exist in the ```OPTSRING``` option and one of the ```case``` statements, then the option will be thrown to the ```default``` case to perform an ```invalid()``` function.

**lastly**, there's a ```case``` statement that will check if the user wanted to perform ```generate()``` using the ```-g``` flag. **with** the AND logical operator (```&&```) in the ```if``` statement, all the other mandatory argument-based flags must be provided, or the script will throw the ```invalid()``` function to warn the user about an incomplete argument. **if** all the arguments don't meet any cases defined in the ```case``` statement, the script will display the ```usage()``` function instead.

**here** is one case for using ```getopts``` in ```testflag-1.sh``` on testing the overall flag to produce the desired output as well as the built-in error handling:

<img src="/images/data/blog/suoofibs-1.gif" width="100%" style="border-radius: 0.5rem;" >

### positional arguments
**in** positional arguments, one of the approaches we take is to create an array called ```args``` first that act as a pool of valid options, including letters and their corresponding keywords. **while** that array stores all the valid arguments, the special variable ```$#``` will store the total arguments that are being passed to the script, which requires at least one flag for the ```while``` loop to run functionally. **here** are the following snippets on the overall usage on positional arguments.

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
case $opt in
  "generate") [[ "$n" && "$a" && "$s" ]] && generate "$n" "$a" "$s" || invalid ;;
esac
#----------
usage
```
**there** are nested ```if``` statements that we will be walking through. **the** first statement in line ```17``` is to check whether the passed raw arguments are using the valid flag format. **it** is determined by checking each argument that at least has the first character as a hyphen. **the** use of double hyphens for a word-based flag isn’t a problem here since it uses a trailing wildcard. **once** it passes, the flag in ```$1``` will be truncated and stored in ```raw_opt``` variable so that it can be compared just by word or letter from the ```args``` array.

**while** the statement at line ```19``` is to check if the flag isn’t ```null```, the last ```if``` statement is used to check whether the flag exists within the ```args``` pool. **the** usage of ```wc``` is going to tell if the ```grep``` command is successful; the output should be ```1```, as it matches the overall operator to be equal to ```1```. **keeping** the positional arguments still in ```$1``` as the flag character or word and ```$2``` as the flag’s value is possible by using the ```shift``` command, which moves the positional arguments to always begin in ```$1``` for all the flag, despite the iteration from the ```while``` loop.

**unlike** using ```getopts```, here we need to create our error handling of invalid flag options that are being provided, which is why we have several ```if``` statements to do so. **since** it can't read a ```default``` case like ```getopts```, we can put those invalid cases in the ```else``` block if the flag isn't matched any of the ```args``` flags. **then** the rest is the same as the ```getopts``` section, which has a specific ```case``` statement to perform the ```generate()``` function if all the mandatory flags are provided.

**here** are one case for using positional arguments as the optional flag in ```testflag-2.sh``` on testing the overall flag, both letter-based and word-based, to produce the desired output as well as the custom error handling:

<img src="/images/data/blog/suoofibs-2.gif" width="100%" style="border-radius: 0.5rem;">

## the verdict is in
**to** have a script that handles kinds of flags, both ```getopts``` and positional arguments servers well in terms of parsing it. **while** ```getopts``` more towards simplicity and readability of the overall workflow, using positional arguments and parsing them manually may give you some form of flexibility, especially the capability to read word-based flags like we used to see on other programs in GNU/Linux. **good** luck with whatever stuff you're doing

## resources
- [testflag-1.sh | **hotpotcookie**](https://github.com/hotpotcookie/hotpotcookie/blob/main/script/blog/testflag-1.sh)
- [testflag-2.sh | **hotpotcookie**](https://github.com/hotpotcookie/hotpotcookie/blob/main/script/blog/testflag-2.sh)

## references
- [Bash Tutorial: getopts | **stackchief**](https://www.stackchief.com/tutorials/Bash%20Tutorial%3A%20getopts)
- [Using --getopts to Pick Up Whole Word Flags - Bash | **AppsLoveWorld**](https://www.appsloveworld.com/bash/100/16/using-getopts-to-pick-up-whole-word-flags)
- [How to Pass Command Line Arguments to Bash Script | **Baeldung**](https://www.baeldung.com/linux/pass-command-line-arguments-bash-script)
- [Beginners Guide to Use getopts in Bash Scripts & Examples | **GoLinuxCloud**](https://www.golinuxcloud.com/bash-getopts/#:~:text=getopt%20vs%20getopts,-getopts%20is%20a&text=The%20main%20differences%20between%20getopts,needs%20to%20be%20installed%20separately)
- [getopts(1p) — Linux Manual Page | **man7**](https://man7.org/linux/man-pages/man1/getopts.1p.html)

---
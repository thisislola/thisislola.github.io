---
layout: post
title: "mdls and its weird kMD items"
subtitle: "the process of creating mdlsx, a wrapper for mdls"
date: 2026-06-04
tags: [mobile, iOS, forensics, tool]
---

Thanks to Sarah Edwards ([mac4n6.com](mac4n6.com)) during the SANS FOR518 course, I discovered the `mdls` command! This is a really interesting command line tool, and while reading about it on this website [https://ss64.com/mac/mdls.html](https://ss64.com/mac/mdls.html) (because I refuse to do `man mdls`) , I found `mdimport` (https://ss64.com/mac/mdimport.html) so doing `mdimport -A` helps  me understand `mdls`. But why do it manually?

I went with a bash script so it wouldn't feel too complicated. I wrote it in the most basic way, this is a first version of what I'm calling `mdlsx`. There was A LOT of trial and error on this, look at how messy this is:

```bash
#!/bin/bash
mdimport -A > /tmp/mdls_descriptions.txt
mdls "$@" | while read line

do
    echo "$line"
    name=`echo $line | awk '{print $1}'`
    desc=`grep "$name" /tmp/mdls_descriptions.txt | head -1 | awk -F'\t' '{print $3}'`

    desc=`echo $desc | tr -d "'"`
    if [ "$name" != "" ] && [ "$desc" != "" ]
    then
        echo " --> $desc"
    fi
done
```

The reason I'm doing `mdimport -A > /tmp/mdls_descriptions.txt` is to avoid the very first version of this:

```bash
describe() {
  case "$1" in
    kMDItemFSName) echo "File name on disk" ;;
    kMDItemDisplayName) echo "Name shown to the user" ;;
    .
    .
    .
```

Anyway, after some more breaking at it, I have shared the end result of `mdlsx` on [this github](https://github.com/thisislola/mdlsx/tree/main).

I like to do explain how to run tools/scripts in a beginner-friendly way because I'm talking to student-me here and I've been confused on this in the past. But the github is more straight forward, so go with that if you'd prefer. Otherwise, if you're still reading, here's the how-to: 


**If you choose to run it, follow these steps** 

1. Download `mdlsx` (no file extension), or create a new file and use copy+paste (save it without an extension)
2. FRom your terminal, go to where the file is and then run `chmod +x mdlsx` (this makes the file executable)
3. Then move it to your path by running this command: `mv mdlsx /usr/local/bin/` 
4. That way you can run `mdlsx` from the terminal! 
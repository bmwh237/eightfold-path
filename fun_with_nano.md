# Fun with `nano`
Chronicling my adventures with Unix-based text editors.
> NOTE: This has been written as though I were writing
>   directly to Dr. Burns.

## Preface

I will start by sying that I initially misunderstood
what I needed to do for this assignment which led to 
some consternation on my end.

My misunderstanding arose from my conflating the idea 
of a **text editor** with a **markup language**. I thought
that we were supposed to use `nano` to create a .md file
and upload that to our repository. I now see that the 
markup language supplies the syntax for editing plain text,
the program that you actually do the editing in is the text
editor.

That being the case, if I were to download one of my .txt
files from my VM and reformat it as .md file, would it display properly?
When I tried this out on my VM with `cat NewFile.md` or 
`cat nanorc.md`, it just displayed the contents as plain text.
Would love to hear feedback on this to know if I'm on the right path,
or way off base.

EDIT: I copied the raw text from my VM instance into `GitHub` and saved
the contents as an .md file and sure enough it translated it correctly!
It seems like text editors are valuable for keeping track of the reason
behind different lines of code, so now I'm curious what file type a code
document would be saved as.

Here's what I mean: in the .nanorc file, `##` doesn't mean "create a heading"
like it does in Markdown, but rather it tells the computer not to read 
that line as a command. I guess I'm just curious what the different languages
are that in this context.

## My Experience with `nano`
I found `nano` to be relatively straightforward. I also downloaded
`micro` because I liked how it looked when you demoed it.

I messed around with `nano` by copying the .nanorc document from 
the text book, and then messed around with a new file using .md
language to see if that would do anything. The only problems I 
ran into were finding the .nanorc file after I saved it (I eventually
realized I couldn't do a basic `ls` command, but rather needed
to do a `ls -a` command to find it) and the `^W` closing out my
VM instance instead of searching the file. I was not aware until 
now that this command closed a program, so that must have been what 
was causing this. If there's any other way search a `nano` file I 
might have to do that since my computer appears to overwrite that
command when I execute it.

Other than that, it was a relatively painless experience coming
to grips with the software. I see the logic of the .nanorc file
and how it uses arguments and commands to make changes to the program,
so I think I know how I can make those kinds of changes in the future
should I want to.

## Conclusion
After initial confusion, I feel like I reached a good base level of comfort
with the `nano` text editor. I might opt to use `micro` in the future, but
either way, I now know what I'm doing and likely won't confuse the terminology
in the future.

Cheers!

# Executing Queries with the `grep` Command
For this exercise I copied the bibliographic and citation information of 13 articles resulting from a search 
for documents about "existentialism" AND "game*" in the Scopus database.  

I decided fairly early on that I wanted to construct one multi-line command that piped in results from previous
commands to create a more refined output. Along the way, I made some cool discoveries and will share them now.
I'm going to structure my post as a line-by-line analysis of my command

## Line 1: `grep -B2 -n "year =" scopus.bib`
To begin with, I wanted to perform a `grep` search that would display the article title, author name, and publication
year (as well as tell me which line of the bib file the information was being pulled from). I focused my search on
the publication year by making the string `"year ="` and then I added the modifiers `-B2` and `-n`, with the former 
displaying the two lines preceding the publication year (author and title) and the latter giving me the line number
from the sopus.bib file, which was of course the document being searched.

## Line 2: `cut -d"=" -f2`
For the sake making the text easier to read, I decided to only display what came after the "=" sign since the content
before it was the same for every line. To do this, I used the `cut` command and indicated = as the delimeter and (`-d"="`), 
while specifying the second field was the information I wanted to keep (`-f2`)

## Line 3: `sed 's/{//' | sed 's/},//' | \`
I initially had some difficulty understanding the syntax of the `sed` command, but I figured it out, and knew I wanted
to incorporate it in my command to solidify the knowledge. The output of my command thus far was much more readable than
it was to begin with, but the text lines stil contained unecessary {brackets} and commas. I used the `sed` command to edit
the text and remove the extraneous markings, figuring out that the / stood for the start of what was being edited and // 
indicated the end of what was edited. In this context, I simply removed the brackets and commas without replacing them.

## Line 4: `grep -Ew "[0-9]{4}"`
Lastly, I was curious if I could perform a `grep` search on the output of my command (since it represented a much more condensed
version of the full scopus.bib file). Initially, I typed `grep -Ew "[0-9]{4}" scopus.bib` to search the "filtered" output, but this
returned the full text of the file. My instinct was then to try and do the same search but remove the file name from the end, figuring
it would then search the piped in information from the previous lines of the command. Sure enough, my hunch was right.

As for what I was trying to do with this search, I simply wanted to highlight the publication years for each entry, so I used `-E` to
allow myself access to the regexp operator and `-w` to limit my searches to full words. My string then was confined to only numbers 
(`[0-9]`) of `{4}` digits.

## Line 5: `tee -a articles.scopus.txt`
Pleased with the presentation of my output, I decided I wanted to preserve it in a .txt file, so I created a file named "articles.scopus.txt" 
using the `touch` command, and attempted to use the `cp` command to copy my results there. However, `cp` only works with two arguments, and 
I technically didn't have an original argument to send the files from. I was stumped

I wracked my brain for a minute and consulted my Linux Command Line book, but wasn't able to find the specific command I needed in this specific
instance. I decided to turn to the internet, and promptly found a forum explaining various ways to go about doing this, ultimately 
landing on the `tee -a` command, which copies the output of a command to the document supplied via the argument and also displays
the results of the command on the screen (that's what the `-a` does).

## Conclusion
Altogether, my command looked like this:
```
grep -B2 -n "year =" scopus.bib | \
cut -d"=" -f2 | \
sed 's/{//' | sed 's/},//' | \
grep -Ew "[0-9]{4}"
tee -a articles.scopus.txt
```
And when I display the contents of the file, here's what it looks like:
```
 Vella, Daniel and Gualeni, Stefano
 Virtual subjectivity: Existence and projectuality in virtual worlds
 2019
--
 Landau, E.
 Existential games in human growth
 1985
--
 Ryall, Emily
 Being-on-the-bench: An existential analysis of the substitute in sport
 2008
--
 Chittaro, Luca and Sioni, Riccardo
 Existential video games: Proposal and evaluation of an interactive reflection about death
 2018
--
 Jones, Ellen D. and Herrick, Charlotte and York, Regina F.
 An intergenerational group benefits both emotionally disturbed youth and older adults
 2004
--
 Kambouris, Manousos E. and Manoussopoulos, Yiannis and Kantzanou, Maria and Velegraki, Aristea and Gaitanis, Georgios and Arabatzis, Michalis and Patrinos, George P.
 Rebooting Bioresilience: A Multi-OMICS Approach to Tackle Global Catastrophic Biological Risks and Next-Generation Biothreats
 2018
--
 Crown, S.
 Communication and abnormal behaviour.
 1979
--
 Vella, Daniel
 Beyond agency: games as the aesthetics of being
 2021
--
 Cartlidge, James
 Interpreting Dwarf Fortress: Finitude, Absurdity, and Narrative
 2024
--
 Yorke, Christopher C.
 ‘The Alexandrian Condition’: Suits on Boredom, Death, and Utopian Games
 2019
--
 Ronkainen, Noora J. and Ryba, Tatiana V.
 Is hockey just a game? Contesting meanings of the ice hockey life projects through a career-threatening injury
 2017
--
 Lundvall, Maria and Lindberg, Elisabeth and Hörberg, Ulrica and Carlsson, Gunilla and Palmér, Lina
 Lost in an unknown terrain: a phenomenological contribution to the understanding of existential concerns as experienced by young women in Sweden
 2019
--
 Leino, Olli Tapio
 Playability and its Absence - A post-ludological critique
 2013
```
I found this process to be really helpful in clarifying my thinking and solidifying my understandin of many of the commands we've learned so far.

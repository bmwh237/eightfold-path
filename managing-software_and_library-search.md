# Modules 3.4: Managing Software and 3.5 Library Search
When it comes to adding and removing software from a Linux distribution, most distributions use what's called a **package manager**
to handle install/uninstall and upgrades of software. Ubuntu uses `dpkg` as its package manager and the advanced package tool,
`apt`, serves as the front-end that we interface with.

## Managing Software

### `sudo` - The Superuser
Funnily enough, there was a gentleman at my library a couple of weeks ago who was using a distribution of Linux to test website
security for his job. We struck up a conversation and I noticed that whenever he was running the command to test a website's
security, he was using `sudo` in his command. I asked him what it was exactly that `sudo` meant, and his response was, "`sudo` 
makes you like a god. You can get in anywhere." I thought it was an entertaining comparison, and is primarily how I think of it now.

In actuality, `sudo` the allows a regular user to become a **superuser** and changes the account to **root** (as in root directory).
This is valuable because a it affords a regular user the ability to perform maintenance on their system.The `sudo` command allows
us to make directories outside of the home (~) directory, for example in /usr/local/bin. 

Our most common usage will probably be using `sudo` in conjunction with the `apt` command, which allows us to look for and install
updates, search for software, and uninstall programs and their dependent software.

### Common `apt` Commands

| **Command** | Description |
| ----------- | ----------- |
| `sudo apt update` | Checks for updates to installed software and compares that list to current versions. Prints a list of the new package information. |
| `sudo apt upgrade` | Will install any upgrades to software that is returned via the `apt update` command. Will be prompted with a Y/N? to proceed with installation |
| `apt search` | *Note: Command does not require `sudo` to run since it doesn't make system modifications.* Searches for a package with a matching name as the argument. Useful for when you want to look for a new piece of software to install. |
| `apt show` | Provides more specific information about the package provided in the argument. |
| `sudo apt install` | Installs the app provided via the argument. |
| `sudo apt remove` | Removes the designated passage. Add `--purge` to remove any configuration files that may have been installed with the app (often in the /etc directory) in order for it to run. Without the contingent software, they are useless. |
| `sudo apt autoremove` | Uninstalls dependencies that may have been installed along with an app. |
| `sudo apt clean` | Removes extra files that are installed with a package, thus freeing up disk space. |

## Library Search

### Exploring the `yaz-client`
Beginning in the 1970s, information retrieval via computers was performed through the Z39.50 protocol. Z39.50 allowed for querying and retrieval of bibliographic information between library databases. The modern-day successors to this archaic tachnology comes to us in the form of SRU (Search/Retrieve via URL) and SRW (Search/Retrieve Web service) and the `yaz-client` allows us to interact directly with these services through the command line.

Installing the `yaz-client` is done via the methods outlined above, so I won't go into detail about my experience with that.

As far as ease of use, the `yaz-client` seems to be quite information dense and I definitely feel like I could spend a long time just trying to learn all the commands. Help can be accessed via a `man` command, but that is also very dense.

To explore a library's OPAC requires access to their server, which one must enter in following the `open` command once they are logged into the `yaz-client`. Once in, queries are performed in much the same way as a database search tool, with one crucial difference being that Booleans are added at the front of the command (or at least, the front after the `find` part). For example, if I wanted to look for books with "information" in the title, and were on the subject of "library science," my command in `yaz` would look like this

```
find @and @attr 1=4 "information" @attr 1=21 "library science"
```

As you can see, the Boolean is in the front of the string, and then the terms proceed afterwards. The @attr bit is a bit different, but its short for attribute and simply designates a field code (title, author, subject, etc). For `yaz`, 1=4 tells the search that you're looking for information in the title and 1=21 tells it that you're looking for information science in the subject headings.

Once you've got your results, `yaz` won't actually present them to you. Instead it will tell you how many results were returned and you simply type `show #` to choose which number result you want to see.

Overall, a very cool that gives me mad respect for the librarians in the 70s and 80s who were on the cutting edge of information retrieval by devising and using this stuff. It also gave me a newfound respect for MARC -- since we mostly see the information from MARC converted in a GUI, its easy to think of it as antiquated, but here its clear that the organization of it does serve a purpose, it's just that that purpose exists at a very foundational level.

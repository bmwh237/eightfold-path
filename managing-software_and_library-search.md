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

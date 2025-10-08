# libpynq-configs
The following will allow you to have a setup where you can write your code on your machine, avoiding the annoying VSCode requiring a restart, and to have IntelliSense. Everything else should work just like libpynq development works according to the website, but you can now do `make deploy` to have the code be uploaded and run on the board. 
## How to set up
Instructions look kinda long but I just wanted to put the commands as clearly as possible whenever possible. It is made so that anyone can figure it out, but I can provide some assistance if I got time (or pay me and I'll set it up for you lol)

- run: `wsl install` on powershell admin terminal 
- Inside wsl: `sudo apt install gcc ssh`
- Install in VSCode the WSL extension
- Copy ssh configs and private keys into wsl at ~/.ssh/ 
	- You also have to `chmod 600 [the key]` in order to use it. 
	- This implies you have private keys set up. Its pretty easy https://pynq.tue.nl/general/ssh-keys/. This guide might not need it but it will be a huge quality of life improver. 
- Installing git on both: 
	- // on the board on ~/libpynq-5EWC0-2023-v0.2.6
	- `touch .gitignore` and paste the contents of the one in this repo into there
	- Replace the contents in (relative path) applications/end.mk with the ones in this repo. You could also just add the deploy definition in the makefile just in case I did an accidental edit to anything else lol. 
	- `git init`
	- `git clone --bare . ~/libpynq.git`
	- `git remote add origin ~/libpynq.git`
	- // on the pc
	- `cd ~`
	- `git clone pynq:libpynq.git libpynq` // assumes pynq is the address to your board
	- `code libpynq`

## Troubleshooting: 
- I cant see the stdout (printf output): it will put the output into your terminal when you do the \n
- It seems to be stuck after running the long ssh command: The board is not properly connected, check for the green light. Unfortunately this doesn't fix the instability of the power delivery. Pro tip, connect the board to a phone charger. In case this is not available just reboot the board until it works :(

## Slightly Technical Note
`make deploy` will be adding some very lackluster git commit messages. You should by all means commit before deploying in order to have some good commit messages. This, however, is rather troublesome when prototyping, explaining the default behavior of this functionality. 


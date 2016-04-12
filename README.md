# Show/Hide files on your Mac

Little script to toggle between shown and hidden files on your Mac.

```bash
try
	do shell script "defaults read com.apple.Finder AppleShowAllFiles"
on error
	display dialog "Couldn't get hidden files' current state. Are they shown or hidden?" buttons {"Shown", "Hidden", "I don't know, get me out of here!"} with title "Warning - Show/Hide files" with icon caution
	
	set result to button returned of result
	
	if result is equal to "Shown" then
		do shell script "defaults write com.apple.finder AppleShowAllFiles TRUE"
	else if result is equal to "Hidden" then
		do shell script "defaults write com.apple.finder AppleShowAllFiles FALSE"
	else if result is equal to "I don't know, get me out of here!" then
		return
	end if
	
end try

set state to do shell script "defaults read com.apple.finder AppleShowAllFiles"

if state is equal to "TRUE" then
	display dialog "Files are shown. What do you want to do?" buttons {"Hide them!", "Do nothing... I'm okay"} default button "Hide them!" with title "Show/Hide files" with icon note
else if state is equal to "FALSE" then
	display dialog "Files are hidden. What do you want to do?" buttons {"Show them!", "Do nothing... I'm okay"} default button "Show them!" with title "Show/Hide files" with icon note
end if

set result to button returned of result

if result is equal to "Show them!" then
	do shell script "defaults write com.apple.finder AppleShowAllFiles TRUE"
else if result is equal to "Hide them!" then
	do shell script "defaults write com.apple.finder AppleShowAllFiles FALSE"
else if result is equal to "Do nothing... I'm okay" then
	return
end if

do shell script "killall Finder"
```

## Installation

* Download [Show-Hide files.dmg](https://github.com/hiulit/show-hide-files-script-mac/blob/master/Show-Hide%20files.dmg?raw=true)
* Open `Show-Hide files.dmg`
* Copy `Show-Hide files.app` to your `/Applications` folder

## Debug/Compile it yourself using AppleScript Editor

Download [Show-Hide files.scpt](https://github.com/hiulit/show-hide-files-script-mac/blob/master/Show-Hide%20files.scpt?raw=true) source code

### Debugging from source code
* Open `Show-Hide files.scpt` with AppleScript Editor.
* Play with it.
* Click the hammer icon to compile it.
* Click the play icon to execute it.

### Compiling into an `.app`
* Open `Show-Hide files.scpt` with AppleScript Editor.
* Go to `File -> Export`.
* Set a name.
* Choose `Application` as the `File format`.
* Click `Save`.

##Changelog

v1.0.0 (April 12th 2016)
* Initial commit

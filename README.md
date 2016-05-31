# Show/Hide files on your Mac

Little script to toggle between visible and hidden files on your Mac.

Here's a glance of the script without localization.

```bash
try
	do shell script "defaults read com.apple.Finder AppleShowAllFiles"
on error
	display dialog "Couldn't get the current state of hidden files. Are they visible or are they hidden?" buttons {"Visible", "Hidden", "I don't know, get me outta here!"} with title "Warning - Show/Hide files" with icon caution
	
	set result to button returned of result
	
	if result is equal to "Visible" then
		do shell script "defaults write com.apple.finder AppleShowAllFiles TRUE"
	else if result is equal to "Hidden" then
		do shell script "defaults write com.apple.finder AppleShowAllFiles FALSE"
	else if result is equal to "I don't know, get me outta here!" then
		return
	end if
	
end try

set state to do shell script "defaults read com.apple.finder AppleShowAllFiles"

if state is equal to "TRUE" then
	display dialog "Files are visible. What do you want to do?" buttons {"Hide them!", "Nothing... It's okay"} default button "Hide them!" with title "Show/Hide files" with icon note
else if state is equal to "FALSE" then
	display dialog "Files are hidden. What do you want to do?" buttons {"Show them!", "Nothing... It's okay"} default button "Show them!" with title "Show/Hide files" with icon note
end if

set result to button returned of result

if result is equal to "Show them!" then
	do shell script "defaults write com.apple.finder AppleShowAllFiles TRUE"
else if result is equal to "Hide them!" then
	do shell script "defaults write com.apple.finder AppleShowAllFiles FALSE"
else if result is equal to "Nothing... It's okay" then
	return
end if

do shell script "killall Finder"
```

## Installation

* Download the [Show-Hide files](https://github.com/hiulit/show-hide-files-script-mac/archive/master.zip) zip file.
* Open `Show-Hide files.dmg`.
* Copy `Show-Hide files.app` to your `/Applications` folder.

## Debug/Compile it yourself using AppleScript Editor

Download the [Show-Hide files](https://github.com/hiulit/show-hide-files-script-mac/archive/master.zip) zip file.

### Debugging from source code
* Open `Show-Hide files.scptd` with AppleScript Editor.
* Play with it.
* Click the **hammer** icon to **compile** it.
* Click the **play** icon to **execute** it.

### Compiling into an `.app`
* Open `Show-Hide files.scptd` with AppleScript Editor.
* Go to `File > Export`.
* Enter a name.
* Choose `Application` as the `File format`.
* Click `Save`.

## Adding translations
* Download the [Show-Hide files](https://github.com/hiulit/show-hide-files-script-mac/archive/master.zip) zip file.
* Right-click on `Show-hide files.scptd` to open the contextual menu and then click on `Show Package Contents`.
* Go to `Contents > Resources` and create a new folder called `<lang>.lproj` (e.g. `de.lproj` for German or `fr.lproj` for French).
* Go to `English.lproj` and copy `Localizable.strings` to the new `<lang>.lproj` recently created.
* Open `Localizable.strings` with your preferred text editor. You'll notice a `"key" = "value";` pattern.
* Translate the `"values"` into the desired language.

PRs are welcome! ;)

##Changelog

### v2.0.0 (May 30th 2016)
* Added localization in Catalan, English and Spanish.

### v1.0.0 (April 12th 2016)
* Initial commit.

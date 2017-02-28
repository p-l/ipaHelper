# ipaHelper script#
==========

Script for examining and resigning ipa files

## COMMANDS

```
ipaHelper profile [file] [options]
ipaHelper find [file] [options]
ipaHelper info [file] [options]
ipaHelper summary [file]
ipaHelper clean [file] [--all]
ipaHelper rezip [output file]
ipaHelper verify [file]
ipaHelper resign [file] [options]
ipaHelper help [options] [command]
ipaHelper open [file]
```
 
### PROFILE 

Checks the profile of an ipa, app, xcarchive, or zip `[file]` containing an app file, or shows the information about a mobileprovision `[file]`
If no `[file]` is provided, the first (alphabetically) `.ipa` file in the working directory is used. If no options are present, a summary of the provisioning profile is displayed.

```
ipaHelper profile [file] [options]

options:
  -v, --verbose 
    display the entire profile in xml format
  -e, --entitlements 
    display the entitlements on the profile
```

### FIND

Looks for profiles saved in the users library matching the bundle ID of the `.ipa`, `.app`, `.xcarchive` or `.zip` file containing an `.app` file. 
If no `[file]` is provided, the first (alphabetically) `.ipa` file in the working directory is used.

```
ipaHelper find [file] [options]

options:
  -m <pattern>, --matching <pattern> 
    only display profiles matching *pattern*
  -n, --no-wildcard  
    only display profiles with exact matches to the bundle ID, and not matching wildcard profiles
  -a, --all
    display all profiles in the users library.  Ignores --no-wildcard option
  --json
    return the profile information in a JSON dictionary
```

### INFO

Checks the `Info.plist` of an `.ipa`, `.app`, `.xcarchive`, or `.zip` file containing an `.app` file, or shows the information about and `Info.plist` file
If no `[file]` is provided, the first (alphabetically) `.ipa` file in the working directory is used.
If no options are present, a summary of the `Info.plist` is displayed.

```
ipaHelper info [file] [options]

options:
  -e <editor>, --edit <editor>
    edit the Info.plist with <editor>. If no <editor> is provided, the default $EDITOR is used.
  -v, --verbose
    display the entire Info.plist in xml format
```

### SUMMARY

Displays profile and info.plist information about an ipa, app, xcarchive, or zip *file* containing an app file.
If no `[file]` is provided the first (alphabetically) `.ipa` file in the working directory is used.

```
ipaHelper summary [file]

options:
  --json
    return the summary information in a JSON dictionary.  Also adds the a key "AppDirectory" for the temporary unzipped app
  -dc, --dont-clean
    do not remove or zip the temporary app directory after returning summary information
```

### CLEAN

Cleans temporary files left over from previous command with the `--dont-clean` option. If run with the `--all` option, the entire temp folder for ipaHelper is deleted. 
If `[file]` is supplied, the folder associated with that file is deleted.

```
ipaHelper clean [file] [options]

options:
  --all
    the entire temp folder for ipaHelper is deleted
```

### REZIP

Rezips left over temporary files from `summary` command with the `--dont-clean` option as `[output file]`. The `[output file]` must be an `.app`, `.ipa`, `.appex`, or `.zip` file.

```
ipaHelper rezip [outputfile]
```

### VERIFY

Checks to make sure the necessary code signing components are in place for an `.ipa`, `.app`, `.xcarchive`, or `.zip` file containing an `.app` file.
If no `[file]` is provided the first (alphabetically) `.ipa` file in the working directory is used.

```
ipaHelper verify [file]
```

### RESIGN

Removes the code signature from an `.ipa`, `.app`, `.xcarchive`, `.appex`, or `.zip` file containing an `.app` file, and replaces it either with the first profile (alphabetically) in the directory with `[file]` or a specified profile (using `-p` option).
Resigns `[file]` using the certificate on the profile and entitlements matching the profile, zips the resigned `.ipa` file with the output filename (`-o` option). 
If no output filename is provided (`-o` option), `[file]-resigned.ipa` is used.
If no `[file]` is provided, the first (alphabetically) `.ipa` file in the working directory is used.

```
ipaHelper resign [file] [options]

options:
  -p <file.mobileprovision>, --profile <file.mobileprovision>
    use mobileprovision file for resigning the ipa
  -f, --find
    look for a profile in the user's library matching the [file]'s bundle ID
  -m <patterns>, --matching <patterns>
    restricts the --find option to only profiles matching <patterns>
  -o <filename>, --output <filename>
    resign the ipa file as <filename> instead of [file]-resigned.ipa
  --overwrite
    overwrites the original file with the resigned file (ignores the --output option)
  -d, --double-check 
    display information about the file, its Info.plist, and the provisioning profile and have be given an option to continue with the resign or quit
  -F, --force
    overwrite output file on resign without asking. Uses the profiles App ID if the App ID and Bundle ID do not match.
```

### OPEN

Copies `[file]` into a temporary file location, unzipped and prints the path to the app file.
If no `[file]` is provided, the first (alphabetically) `.ipa` file in the working directory is used.

```
ipaHelper open [file]
```

### HELP

Displays usage information for the commands.

```
ipaHelper help [options] [command]
  -v option is present it shows the usage information for all of the commands.
```

## AUTHOR

Marcus Smith

## ORIGINAL SOURCE

[https://github.com/MarcusSmith/ipaHelper](https://github.com/MarcusSmith/ipaHelper)
# Changelog

All notable changes to this project will be documented in this file.

The format is based on [Keep a Changelog](https://keepachangelog.com/en/1.0.0/)

## [Version 1.7.0](https://github.com/robweber/xbmcbackup/compare/matrix-1.6.8...robweber:matrix-1.7.0)

### Added

- You can now append a suffix to the end of each backup name (folder or zip file). This is only available in the Advanced or Expert settings.
- validation file now saves a list of all installed addons and versions
- prompt to close Kodi at the end of successful restore

### Changed

- added new line between file size and file name, was unreadable on some systems due to string resizing
- modified GitHub issue template slightly
- translations sync
- token files are stored in a `.json` instead of a `.txt` file
- file discovery process now flags directories with an `is_dir` metadata property instead of prefixing with a dash (-). This was done for legacy reasons and there is no reason for it.

### Fixed

- fixed minor UI issues
- division error when transferSize = 0
- fixed Dropbox tokens expiring by using [refresh tokens](https://dropbox-sdk-python.readthedocs.io/en/latest/api/oauth.html)

## [Version 1.6.8](https://github.com/robweber/xbmcbackup/compare/matrix-1.6.7...robweber:matrix-1.6.8)

### Changed

- use the `<source>files</source>` tag on the remote path browser to bring in saved file paths from the File Manager
- multiple language files updated through integration with [Weblate](https://kodi.weblate.cloud/projects/kodi-add-ons-scripts/script-xbmcbackup/), thanks to @gade01 for helping to get it working.

### Fixed

- default en_gb file must use empty `msgstr` value
- minor UI fixes for dialog prompts
- fixed catch22 situation where Dropbox remote tries to load prior to authorization flow
- travis CI links in README

## [Version 1.6.7](https://github.com/robweber/xbmcbackup/compare/matrix-1.6.5...robweber:matrix-1.6.7) - 2021-04-16

### Added

- added QRcode when setting up Dropbox, uses pyqrcode

### Fixed

- fixed issue when using ```RunScript()``` within settings to launch Advanced Editor
- error on advanced settings restore prior to reboot
- minor gui dialog fixes

## [Version 1.6.6](https://github.com/robweber/xbmcbackup/compare/matrix-1.6.5...robweber:matrix-1.6.6) - 2021-03-15

### Fixed

- error when typing the remote path, ```listBackups()``` function was not working if final slash not included in typed directory path name.
- added ```force=True``` flag to the ```rmdir()``` function. Fixes issue with directories being removed when not empty

## [Version 1.6.5](https://github.com/robweber/xbmcbackup/compare/matrix-1.6.4...robweber:matrix-1.6.5) - 2021-03-06

### Added

- added Expert setting to change location of zip file temp location as it's being built or extracted

### Changed

- updated ```settings.xml``` to match new [Kodi settings syntax](https://kodi.wiki/view/Add-on_settings_conversion), including visibility levels

### Fixed

- when restoring from a zip file the command to delete the extracted directory was incorrect
- ```Dialog().yesno()``` no longer takes line1 arg, changed to message

## [Version 1.6.4](https://github.com/robweber/xbmcbackup/compare/matrix-1.6.3...robweber:matrix-1.6.4) - 2020-12-23

### Added

- merged duplicate copy code into ```_copyFile``` method
- added method to backup/restore Kodi settings via the GetSettings/SetSettingValue JSON methods in the validation file
- added setting to always restore settings or prompt at the time of backup

### Changed

- updated script.module.future version to current
- swapped xbmc.translatePath for xbmcvfs.translatePath, deprecated

### Fixed

- fixed calls to ```xbmcgui.Dialog().ok()```, method definition changed to only allow one message arg with Kodi 19
- fixed import of dropbox Oauth package in authorizer flow

### Removed

- removed old xml GuiSettings parsing for settings restore

## [Version 1.6.3](https://github.com/robweber/xbmcbackup/compare/matrix-1.6.2...robweber:matrix-1.6.3) - 2020-06-15

### Changed

  - fixed validatePath error (issue #166) thanks (thanks @AnonTester)

## [Version 1.6.2](https://github.com/robweber/xbmcbackup/compare/matrix-1.6.1...robweber:matrix-1.6.2) - 2019-04-09

### Changed

  - changed PNG screenshots to JPG (per [#165](https://github.com/robweber/xbmcbackup/issues/165))

## [Version 1.6.1](https://github.com/robweber/xbmcbackup/compare/matrix-1.6.0...robweber:matrix-1.6.1) - 2019-12-30

### Added

  - added method to get size of a file from the VFS
  - added total transfer size information to progress bar with appropriate precision (KB, MB, etc)
  - show file size of zip files in the restore selection dialog
  - added getSettingInt and getSettingBool to utils.py class
  - added verbose logging setting and tied it to logging related to file paths added/written, this will significantly reduce the debug log size (thanks CastagnaIT)
  - localize advanced editor strings instead of hard coding English

### Changed

  - display every file transfered in progress bar, not just directory
  - base progress bar percent on transfer size, not total files
  - changed getSettings where needed to getSettingBool and getSettingInt
  - use service.py to start scheduler, moving scheduler to resources/lib/scheduler.py Kodi doesn't cache files in the root directory
  - fixed issues with rotating backups where trailing slash was missing (thanks @AnonTester)
  - read/write files using contextlib

## [Version 1.6.0](https://github.com/robweber/xbmcbackup/compare/krypton-1.5.2...robweber:matrix-1.6.0) - 2019-11-26

### Added

 - added new badges for Kodi Version, TravisCI and license information from shields.io
 - dependency on script.module.dateutil for relativedelta.py class

### Changed

 - addon.xml updated to use Leia specific syntax and library imports
 - removed specific encode() calls per Python2/3 compatibility
 - call isdigit() method on the string directly instead of str.isdigit() (results in unicode error)
 - added flake8 testing to travis-ci
 - updated code to make python3 compatible
 - updated code for pep9 styling
 - use setArt() to set ListItem icons as the icon= constructor is deprecated
 - Dropbox dependency is now 9.4.0

### Removed

 - removed need for urlparse library
 - Removed GoogleDrive support - issues with python 3 compatibility
 - removed relativedelta.py, use the dateutil module for this

## [Version 1.5.2](https://github.com/robweber/xbmcbackup/compare/krypton-1.5.1...robweber:krypton-1.5.2) - 2019-09-30

### Added

 - Updated Changelog format to the one suggested by [Keep a Changelog](https://keepachangelog.com/en/1.0.0/)
 - Added script.module.dropbox import as a dependency for Dropbox filesystem

### Changed

 - Fixed issue getting xbmcbackup.val file from non-zipped remote directories. Was being copied as though it was a local file so it was failing.
 - Use linux path separator (/) all the time, Kodi will interpret this correctly on windows. Was causing issues with remote file systems since os.path.sep
 - Fixed minor python code style changes based on kodi-addon-checker output

### Removed

 - files releated to dropbox library, using script.module.dropbox import now

## Version 1.5.1 - 2019-09-10

### Changed
 - Fixed guisettings restores not working - thanks Bluerayx

## Version 1.5.0 - 2019-08-26

### Added
- Added new Advanced file editor and file selection based on a .json

### Removed
- File backups and restores will not work with old version - breaking change with previous versions PR117

## Version 1.1.3 - 2017-12-29

### Added
 - added file chunk support for Dropbox uploads
 - added scheduler delay to assist with time sync (rpi mostly), will delay startup by 2 min

### Changed
 - fixed settings duplicate ids, thanks aster-anto

## Version 1.1.2

### Added
 - Fixes to the Dropbox lib for python 2.6

## Version 1.1.1

### Added
 - added ability to "catchup" on missed scheduled backup

### Changed
 - fixed error on authorizers (missing secret/key)
 - updated google oauth and client versions
 - merged in dropbox v2 library code

## Version 1.1.0

### Added
 - added tinyurl generation for oauth urls

### Changed
 - moved authorize to settings area for cloud storage

## Version 1.0.9

### Changed
 - fixed dropbox rest.py for Python 2.6 - thanks koying!

## Version 1.0.8

### Changed
 - updated dropbox api

## Version 1.0.7

### Changed
 - updated google client api version

## Version 1.0.6

### Added

 - added progress for zip extraction - hopefully helps with extract errors

### Changed
 - fix for custom directories not working recursively

## Version 1.0.5

### Added
 - added google drive support
 - added settings dialog option - thanks ed_davidson

### Changed
  - make compression setting compatible with python 2.6 and above
  - fix for growing backups - thanks brokeh

## Version 1.0.4

### Added
 - exit if we can't delete the old archive, non recoverable

## Version 1.0.3

### Added
 - added "delete auth" dialog to delete oauth files in settings

## Version 1.0.2

### Changed
 - updated xbmc.python version to 2.19.0 - should be helix only

## Version 1.0.0

### Changed
 - rebranded as "Backup"
 - removed XBMC references and replaced with Kodi
 - tweaked file walking for Helix

## Version 0.5.9

### Added

 - create restored version of guisettings for easy local restoration

### Changed
 - fixed dropbox unicode error

## Version 0.5.8.7

### Added
 - allow limited updating of guisettings file through json

## Version 0.5.8.6

### Added
 - show notification if some files failed
 - check if destination is writeable - thanks war59312

## Version 0.5.8.5

### Added
 - added custom library nodes to config backup options - thanks Ned Scott

## Version 0.5.8.4

### Changed
 - backup compression should use zip64 as sizes may be over 2GB
 - need to expand out path -bugfix

## Version 0.5.8

 - fixes path substitution errors

## Version 0.5.7

 - added option to compress backups, uses local source for staging the
   zip before sending to remote

## Version 0.5.6

 - fix dropbox delete recursion error - thanks durd updated language
   files

## Version 0.5.5

 - fix for dropbox errors during repeated file upload attempts

## Version 0.5.4

 - check xbmc version when doing a restore

## Version 0.5.3

 - updated python version

## Version 0.5.2

 - added additional script and window parameters, thanks Samu-rai
 - critical error in backup rotation
 - updated progress bar display

## Version 0.5.1

 - updated for new Gotham xbmc python updates

## Version 0.5.0

 - New Version for Gotham

## Version 0.4.6

 - modified backup folder names to include time, also modified display
   listing

## Version 0.4.5

 - added version info to logs
- added try/catch for unicode errors

## Version 0.4.4

 - modified the check for invalid file types

## Version 0.4.3

 - added error message if remote directory is blank
 - added license tag

## Version 0.4.2

 - Added support for userdata/profiles folder - thanks TUSSFC

## Version 0.4.1

 - added encode() around notifications

## Version 0.4.0

 - fixed settings display error - thanks zer04c

## Version 0.3.9

 - added "just once" scheduler for one-off type backups
 - show  notification on scheduler  
 - update updated language files from  Transifex

## Version 0.3.8

 - added advancedsettings check on restore. prompts user to restore only this file and restart xbmc to continue. This fixes issues where path substitution was not working during restores - thanks ctrlbru

## [Version 0.3.7]

 - added optional addon.xml tags
 - update language files from Transifex

## Version 0.3.6

 - added up to 2 custom directories, can be toggled on/off
 - added a check for backup verification before rotation - no more
   deleting non backup related files
 - use monitor class for onSettingsChanged method

## Version 0.3.5

 - test of custom directories - only 1 at the moment

## Version 0.3.4

 - added ability to take parameters via RunScript() or
   JSONRPC.Addons.ExecuteAddon()

## Version 0.3.3

 - updated xbmc python version (2.1.0)

## Version 0.3.2

 - added settings for user provided Dropbox key and secret

## Version 0.3.1

 - added try/except for multiple character encodings
 - remove token.txt file if Dropbox Authorization is revoked
 - can shutdown xbmc after scheduled backup

## Version 0.3.0

 - major vfs rewrite
 - Added Dropbox as storage target
 - updated gui/removed settings - thanks SFX Group for idea!

## Version 0.2.3

 - first official frodo build

## Version 0.2.2

 - fix for backup rotation sort

## Version 0.2.1

 - added ability to rotate backups, keeping a set number of days

## Version 0.2.0

 - removed the vfs.py helper library
 - default.py file now uses xbmcvfs python library exclusively for
   listing directories and copy operations

## Version 0.1.7

 - minor bug fixes and translations updates

## Version 0.1.6

 - merged scheduler branch with master, can now schedule backups on an
   interval

## Version 0.1.5

 - pulled xbmcbackup class into separate library

## Version 0.1.4

 - added more verbose error message for incorrect paths

## Version 0.1.3

 - backup folder format - thanks zeroram
 - added German translations - thanks dersphere
 - removed need for separate verbose logging setting
 - updated utf-8 encoding for all logging
 - backup now uses date as folder name, restore allows user to type date
   of last backup

## Version 0.1.2

 - added French language translation - thanks mikebzh44
 - added some utf-8 encoding tags to filenames

## Version 0.1.1

 - added check for key in vfs.py - Thanks Martijn!

## Version 0.1.0

 - removed transparency from icon.png

## Version 0.0.9

 - modified vfs.py again to filter out xsp files (smart playlists).
   Created running list for these types of compressed files
 - added enable/disable logging toggle in settings

## Version 0.0.8

 - modified vfs.py script to exclude handling zip files as directories,
   added keymap and peripheral data folders in the "config" section

## Version 0.0.7

 - removed "restore.txt" file and now write file listing to memory list
   instead

## Version 0.0.6

 - Added the vfs module created by paddycarey
 - File Selection is now followed for both backup and restore options

## Version 0.0.5

 - Added option to manually type a path rather than browse for one (only
   one used)
 - Show progress bar right away so you know this is doing something

## Version 0.0.4

 - Finished code for restore mode.

## Version 0.0.3

 - Added progress bar and "silent" option for running on startup or as a
   script

## Version 0.0.2

 - First version, should backup directories as needed

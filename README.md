

# How to deploy in Heroku?
Hit the deploy to heroku button and follow the further instructions in the screen:

**NB: Usage of Aria2 may leads to the suspension of your heroku account so deploy at your own risk.**

[![Deploy](https://www.herokucdn.com/deploy/button.svg)](https://heroku.com/deploy?template=https://github.com/iamjuander/magneto-heroku)

# Important - Read these points first
- Original repo is https://github.com/lzzy12/python-aria-mirror-bot
- I have collected some cool features from various repositories and merged them in one.
- So, credits goes to original repo holder, not to me. I have just collected them.
- This (or any custom) repo is not supported in official bot support group.
- So if you have any issue then check first that issue is in official repo or not, You are only allowed to report that issue in bot support group if that issue is also present in official repo.

## Credits :-
- First of all, full credit goes to [Shivam Jha aka lzzy12](https://github.com/lzzy12) He build up this bot from scratch.
- Then a huge thanks to [Sreeraj V R](https://github.com/SVR666) You can checkout his [repo here](https://github.com/SVR666/LoaderX-Bot)
- Features added from [Sreeraj V R's](https://github.com/SVR666) repo -
```
1. Added Inline Buttons
2. Added /del command to delete files from drive
3. /list module will post search result on telegra.ph
```
- Special thanks to [archie](https://github.com/archie9211) for very much useful feature **Unzipmirror**
- Features added from [archie's](https://github.com/archie9211) repo
```
1. unzip
2. Update tracker list dynamically
3. Fix SSL handsake error
```

# What is this repo about?
This is a telegram bot writen in python for mirroring files on the internet to our beloved Google Drive.

# Inspiration 
This project is heavily inspired from @out386 's telegram bot which is written in JS.

# Features supported:
- Mirroring direct download links to google drive
- Mirroring Mega.nz links to google drive (In development stage)
- Mirror Telegram files to google drive
- Mirror all youtube-dl supported links
- Extract these filetypes and uploads to google drive
> ZIP, RAR, TAR, 7z, ISO, WIM, CAB, GZIP, BZIP2, 
> APM, ARJ, CHM, CPIO, CramFS, DEB, DMG, FAT, 
> HFS, LZH, LZMA, LZMA2, MBR, MSI, MSLZ, NSIS, 
> NTFS, RPM, SquashFS, UDF, VHD, XAR, Z.
- Copy files from someone's drive to your drive (using Autorclone)
- Service account support in cloning and uploading
- Download progress
- Upload progress
- Download/upload speeds and ETAs
- Docker support
- Uploading To Team Drives.
- Index Link support
- Shortener support

## Bot commands to be set in botfather

```
darpan - Start Mirroring
tar - Upload tar (zipped) file
unzip - Extract files
clone - copy folder to drive
watch - mirror YT-DL support link
tarwatch - mirror youtube playlist link as tar
kill - Cancel a task
killall - Cancel all tasks
del - Delete file from Drive
list - [query] searches files in G-Drive
status - Get Mirror Status message
stats - Bot Usage Stats
help - Get Detailed Help
log - Bot Log [owner only]
```
 
## Getting Google OAuth API credential file

- Visit the [Google Cloud Console](https://console.developers.google.com/apis/credentials)
- Go to the OAuth Consent tab, fill it, and save.
- Go to the Credentials tab and click Create Credentials -> OAuth Client ID
- Choose Desktop and Create.
- Use the download button to download your credentials.
- Move that file to the root of mirror-bot, and rename it to credentials.json
- Visit [Google API page](https://console.developers.google.com/apis/library)
- Search for Drive and enable it if it is disabled
- Finally, run the script to generate token Google Drive:
```
pip3 install google-api-python-client httplib2 oauth2client
python3 generate_drive_token.py
```

# Using service accounts for uploading to avoid user rate limit
For Service Account to work, you must set USE_SERVICE_ACCOUNTS="True" in config file or environment variables
Many thanks to [AutoRClone](https://github.com/xyou365/AutoRclone) for the scripts
## Generating service accounts
Step 1. Generate service accounts [What is service account](https://cloud.google.com/iam/docs/service-accounts)
---------------------------------
Let us create only the service accounts that we need. 
**Warning:** abuse of this feature is not the aim of autorclone and we do **NOT** recommend that you make a lot of projects, just one project and 100 sa allow you plenty of use, its also possible that overabuse might get your projects banned by google. 

```
Note: 1 service account can copy around 750gb a day, 1 project makes 100 service accounts so thats 75tb a day, for most users this should easily suffice. 
```

`python3 gen_sa_accounts.py --quick-setup 1 --new-only`

A folder named accounts will be created which will contain keys for the service accounts created

NOTE: If you have created SAs in past from this script, you can also just re download the keys by running:
```
python3 gen_sa_accounts.py --download-keys project_id
```

### Add all the service accounts to the Team Drive or folder
- Run:
```
python3 add_to_team_drive.py -d SharedTeamDriveSrcID
```

# Youtube-dl authentication using .netrc file
For using your premium accounts in youtube-dl, edit the netrc file (in the root directory of this repository) according to following format:
```
machine host login username password my_youtube_password
```
where host is the name of extractor (eg. youtube, twitch). Multiple accounts of different hosts can be added each separated by a new line

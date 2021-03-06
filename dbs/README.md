# Local database description
MOST FILES AND FOLDERS INSIDE THE '[homedir]/.skyscraper/dbs' FOLDER ARE NOT MEANT TO BE MANIPULATED BY HAND!!! It can be done, but don't complain to me about the format of the database. It is NOT meant to be understood by humans. It is meant to be efficient for reading and parsing by Skyscraper itself. Same goes for the media files that reside in the subfolders.

## Don't leave custom files in here
If you decide to add your own files to the subfolders, you risk them being deleted by Skyscraper later on if it is run with the '--cleandb' command line option. You've been warned! :)

## The mandatory exception to the rule
There is ONE file that you can and should edit inside each of the platform db folders. That file is called 'priorities.xml' and decides the scraper priority of resources for each resource type. For instance, if you know that 'thegamesdb' always provides the best 'descriptions' for games, you'd add an '`<order type="description">`' node with a '`<source>thegamesdb</source>`' subnode. You can have multiple '`<source>`' nodes, Skyscraper will then prefer the topmost source when scraping with the 'localdb' (set with '-s localdb') scraping module. If the topmost isn't found, it'll use the next one and so on. If no 'priorities.xml' file is found, it will prioritize using timestamps.

Skyscraper provides the example file 'priorities.xml.example' residing in this directory. To use it, copy it to any platform db subfolder (for instance, copy it to '[homedir]/.skyscraper/dbs/nes/priorities.xml') and edit it to your liking. Be sure to remove the '.example' part of the filename so it's just called 'priorities.xml'.

## Other cool stuff you CAN DO
And what I encourage you to do! :) Each subfolder in this folder is self-contained and can be copied to your friends at your convenience. Just zip it up or copy the folder itself over to some other computer that has Skyscraper 1.6.0 or later installed, and you can make use of the data using the '-s localdb' scraping module option. If you add it at a non-default location, set the db folder with '-d [dbfolder]'.

Keep in mind that you need to unzip the folder before using it. Skyscraper currently does not support zipped db's (and might not ever, I haven't decided on this yet).

## To those who live the thug life
... and decide to completely ignore my warnings. If you absolutely insist on editing the databases by hand (DON'T!), here's a description of the format. It's really, really simple. (It is, but DON'T!)

### Sha1 primary key
The database consists of sha1 summed entry resources. The sha 1 sum is calculated from the rom data or, in special cases, the filename (in cases where the file data is a script or similar). An entry can look like this:

```xml
<resource sha1="[sha1 sum]" type="[resource type]" source="[scraping source]" timestamp="[msecs sine epoch]">Resource data</resource>
```

### Resource types
#### title
A game title
#### platform
A game platform
#### description
A game description
#### publisher
The publisher of a game
#### developer
The developer of a game
#### players
How many players are supported by a game
#### tags
List of game tags, most often genre related
#### releasedata
The release data of a game
#### rating
Game rating, number between 0 and 1
#### cover
A cover image filename for a game (file exists in 'covers' subfolder)
#### screenshot
A screenshot image filename for a game (file exists in 'screenshots' subfolder)
#### video
A video file filename for a game (file exists in 'videos' subfolder)

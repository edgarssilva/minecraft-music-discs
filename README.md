# How to setup a Minecraft Server with Custom Music Discs

This is a tutorial on how to setup a Minecraft server with custom music discs using Spigot Plugins.

There will be no need to follow most this tutorial since I will provide everything completed until the creating of the music discs but feel free to read it all. 

Created By [Edgar Silva in Upwork](https://www.upwork.com/o/profiles/users/~01e90c92bb5295859e/) for **Tom Schnitz**.

# Download Spigot

First you download the latest build version of Spigot in here: [Get Bukkit](https://getbukkit.org/)

That will download a file called spigot-x-x-x.jar (**x** is the server version).

Setup a folder for the server and move the jar there and rename it to a simpler name like **server**.

> **Note:** This is already setup for you but in case you want to update your Minecraft Server this is what you need to do

## Create a bat file

Now to run the server you need to create a **run.bat** file with the following content:
```
	java -jar server.jar -nogui
	pause
```
In this case we used **server.jar** you need to rename it to whatever you renamed the file before.

Now just run the file.

## EULA

After you run the server it will close itself because you need to accept the EULA, to do that open the eula.txt file and change the *eula=false* to *eula=true*.

Now you can run the server again it setup the world and everything else.

## Adding Plugins

At this point, you have a fully working vannila Minecraft Server so feel free to change the **server.yml** file and others as wish.

But to add the juicy stuff you will want to download some plugins, for the custom music discs we will use one called [Jukebox Extended](https://www.spigotmc.org/resources/jukebox-extended-add-custom-music-disc.76963/) feel free to check it out.

To setup the plugin you need to go into it's website and download it as aswell as it's dependency [ProtocolLib](https://www.spigotmc.org/resources/protocollib.1997/).
>**Note:** This will already be setup for you but if you wanna update or setup new plugins this is the way to do it.

After that move the plugins into the **plugins** folder and run the server.
>**Note:** If you don't see a plugins folder run the server once so it gets created

# Creating a Resource Pack

For the server to be able to have custom music it will need to have it's own **resource pack** but this has some disadvantages. To ensure everyone is using the resource pack the plugin will ask everyone that wasn't able to download it to reconnect to the server, you can disable and change the messages in the plugins configuration.
Another "issue" is a when you connect and disconnect from the server you will get a very fast Mojang loading screen while it loads the pack. But for most that won't be a problem.

## Folder Structure

If you ever opened a resource pack you can see this is basicly a bunch of folders and **.json** files with textures, sounds, language packs etc. The way resource packs work is every asset in you pack will override the default one, so if you don't override anything it will just be a default pack. You can learn more about them in [this link](https://minecraft.gamepedia.com/Resource_Pack).
In this case we just want to add new music records.  So you wil need to create the folders and files listed below:
```
.
|	📂 assets
|	|   📂 minecraft
|	|   |	📂 sounds
|	|   |	|	📂 records
|	|   |	|	|	🎵 your_song.ogg
|	|   |	|	|	🎵 your_song2.ogg
|	|   |	📜 sounds.json
📜 pack.mcmeta
📷 pack.png
```
As you can see there some files that need to be created, I will explain each one on the next sections.

## Pack.png

Let's start by the **pack.png** file, this needs to be a *256x256* image of you pack. 

<p align="center">
	<img src="https://lh3.googleusercontent.com/f6asStlNvrNZ0e4cqu5zbhnZ_u0WTTdWxfF9O29BQuOFXZmwPAg7T04CJ3Bp64p0SWCU7Osmn7I"   />
	<br>Minecraft Default Pack
</p>

## Pack.mcmeta

The **pack.mcmeta** is just a **.json** file with some basic information about the pack, so create the file with the following:

```
{
	"pack": {
		 "pack_format": 6,
	     "description": "Your Custom Pack Description"
	  }
}
```
## Creating a music file

Minecraft audio files can't be in just any file type they are **.ogg** files and need to be in **mono** so you it can lower its volume depeding from how fair you are and also play in the right ear depeding on what side your facing.

In order to convert the file I would use a program like **audacity**  but easiest way is to use a online conversion tool like this one [Online OGG converter](https://audio.online-convert.com/convert-to-ogg).
So open the link choose the file you want to convert, also on the **"Change audio channels:"** option choose **mono**.

Once you got your **.ogg** files drop them in the corrent folder shown above.

## Sounds.json
This is the most important file since it's the one that says where each music file is and what it's called. On this example I will use a portion of the song **Brain Power** and a "blank" example.

```
{
	  "noma.brainpower": {
		"sounds": [
			{
			  "name": "records/brainpower",
			  "stream": true
			 }
		]
	},
	"artist.songname": {
		"sounds": [
			{
				"name": "records/your_song",
				 "stream": true
			}
		]
	}
}
```

You can indent the file in any way you want but make sure u have the right json syntax, if you jsut want to copy make sure u have the exact same amount of () and {}. 
Keep in mind that you need remember the **namespace** you gave each sound, in this case **"noma.brainpower"** with *noma* beeing the artist and *brainpower* the song.  The *name* property is the path to the **.ogg** file starting in the **sounds** folder.

>**Note:** You can add as many musics you want just make sure to respect the json syntax.

## Uploading the Resource Pack

In order for the resource pack to be loaded it needs to be in a **.zip** file. Assuming you have **WinRar** you can select the pack.png, pack.mcmeta and the assets folder and zip it.

Now you need to upload the zip file somewhere online where you can get a direct download link.
I would for ease of use upload the zip to a Google Drive account share it then use [this link](https://sites.google.com/site/gdocs2direct/home) to get a direct download link.

Once you do that you can go to your **server.yml** file  and find the line with resource pack and replace with:

    resource-pack=https://drive.google.com/uc?export=download&id=1YsmyD2Y_5vmRjdAwnKSEjVOjJzTLLLEm

>**Note:** This link is just an example

# Configuring the Plugin

After you guys everything setup and the plugins on the right folder all that it's left to do is add the new sounds to the plugin, and maybe configure some settings.

To do that open the **plugins** folder then the **JukeboxExtended** in there you will see a file called **config.yml**, it will look something like this:
```
jext:
  # Kick players who decline server resource pack
  force-resource-pack: true

  # Kick message for rejecting server resource pack
  resource-pack-decline-kick-message: "Please enable resource pack for the music!"

  # Ignore if player somehow failed downloading the resource pack
  ignore-failed-download: false

  # Kick message for player who failed downloading the resource pack
  failed-download-kick-message: "Resource pack download failed, please re-join to try again."

  # Allow/Disallow overlapping music (two jukebox playing same music together)
  allow-music-overlapping: false

  # Register your discs here
  disc:
    "Cat": 
      namespace: "music_disc.cat"
      author: "C148"
      model-data: 0
      creeper-drop: true
      lore:
        - "Minecraft originals"
    "Stal":
      namespace: "music_disc.stal"
      author: "C148"
      model-data: 0
      creeper-drop: true
      lore:
        - "Minecraft originals"
```

As you can see there are 2 demo discs already created, to add a new you you can just copy one of them bellow and change some values.
The first property is the *name* of the disc, the *namespace* is the important part here, remember that namespace you created in the **sounds.json**, well you will need to use it now. 
Then you have some simple properties like the *author*,  *model-data*, *creeper-drop* and *lore* that is basicly a description of an item in Minecraft. The only weird one here is the *model-data* that is basicly a property to change the icon of the disc if you do wish to change the icon read [this](https://github.com/Tajam/jext-spigot-plugin/wiki/4.-Configuration-Guide#custom-model-data) (by default its the broken disc).

So following the example above you would have to do something like this:
```
"BrainPower":
      namespace: "noma.brainpower"
      author: "noma"
      model-data: 0
      creeper-drop: true
      lore:
        - "A cool song that gives power to your brain"
```
>**Note:** This a yaml file so make sure you follow the right syntax

# Using the Plugin

At this point the plugin should be working the only thing left is to try it out. Run the server and join in.

Now you can run commands using **/jukeboxextended** as long you are an operator (/op). If you want to play music wherever you go you can run the command **/jukeboxextended:playmusic Username noma.brainpower**, username beeing the persons *name* and *nom.brainpower* the music. Same can be done to give discs and alot more.

Enjoy 🎵🎶🎵

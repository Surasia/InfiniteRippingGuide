# Halo Infinite Model Ripping Guide

## Required Software
- [Blender](https://www.blender.org/download/)
    - [blender-halo-infinite](https://github.com/Coreforge/blender-halo-infinite) 
    - [Halo Infinite Modular Shader](https://cdn.discordapp.com/attachments/1035019724444160081/1035019728445505656/HIMS_2.7.blend)
- [HaloInfiniteModuleUnpacker](https://github.com/Surasia/HaloInfiniteModuleUnpacker)
- [HaloInfiniteModelExtractor](https://github.com/MontagueM/HaloInfiniteModelExtractor)
- [XNConvert](https://www.xnview.com/en/xnconvert/)
- [InfiniteRuntimeTagviewer](https://github.com/Gamergotten/Infinite-runtime-tagviewer)
- [InfiniteCoatingTool](https://github.com/Surasia/Infinite-Coating-Tool/releases/tag/release)
- [HaloInfiniteResearch](https://github.com/urium1186/HaloInfiniteResearch/tree/develop)
- [Python](https://www.python.org/downloads/release/python-3111/)
- [Halo Infinite](https://store.steampowered.com/app/1240440/Halo_Infinite)

## Unpacking Modules
To actually extract models or any data from the game, we need to uncompress it. For this, download HaloInfiniteModuleUnpacker and extract it to a directory. Open "unpacker.py" in Python's IDLE or any other text editor. Now scroll to the bottom of the .py file, where you will see "unpack_path" and "deploy_path".

> For "unpack_path" enter any directory of your choice which has more than 50GBs of space. It is recommended to have it close to the root of your drive.

> For "deploy_path", navigate to your Halo Infinite install and copy the path for the "deploy" path folder.

**Important: Make sure you have use forward slashes (/) and have no backwards slashes present (\\).**

After you've entered the directories, you can now run the script. In IDLE, you can use the Run > Run Module option, or manually run it using cmd (py unpacker.py). You should now see the modules slowly listing their file amounts and extracting themselves to the given unpack path.

![image](https://user-images.githubusercontent.com/74399067/206862389-6b20ca1f-7579-41ad-a7ad-cd8753d5f356.png)

## Extracting Textures
For texture extraction, we need to use HaloInfiniteMOdelExtractor. Download it and extract it to a directory of your choice. Now open the bitmap_to_dds.py file and again scroll to the bottom of the file. Here, you will see three variables to edit.

> For "unpack_directory" use the "unpack_path" from the previous step.

> For "directory" you can specify a folder to extract in your unpack path, however I recommend just entering f"{unpack_directory}" which will extract everything in your unpack path.

> For "out_path", you can enter any directory you want, however for ease sake I recommend using "unpack_path" again.

After you've entered the directories, you can now run the script. In IDLE, you can use the Run > Run Module option, or manually run it using cmd (py unpacker.py). You should now see textures being extracted and .dds files appearing in the directories listed.

![image](https://user-images.githubusercontent.com/74399067/206863140-564ac3ba-d506-45f0-81ca-30e15ba45eb9.png)

## Converting DDS to PNG
While DDS files are good for compression in games, the limited support of it outside of engines can cause issues, especially with Blender. For this, we can convert our files to PNG or TGA using XNConvert, which can batch thousands of files quickly. 

To convert your textures, simply open XNConvert and drag a folder from your unpack directory into it, go to output, select "Delete Original", enable "Use Multiple CPU Cores" with the maximum amount of threads, and set "Format" as PNG.

In this example, I used "elite" from the "\__chore\pc__\objects\characters" folder and dragged it into XnConvert.
![](https://user-images.githubusercontent.com/74399067/206863613-c79ebffc-fc6e-4fa2-8c43-a3c830a145db.gif)

## Importing Models 
For this step, you will need Blender and the blender-halo-infinite addon by Coreforge. To install the addon, go to Edit, Preferences, Add-ons and then select the zip you downloaded. You do not need to unzip the file for this step.

![](https://user-images.githubusercontent.com/74399067/206867790-e1e0439e-1f34-4a0b-9cf9-bada0ff8be2c.gif)

Now, in blender, go to File, import and select "Halo Infinite rendermodel". Now, using the explorer in blender, navigate to your unpack folder. Models are most commonly found in the "\_chore\gen__\" directory. Here, go into the folder which has the model that you want to import. 

For this example, I used the Grapple Shot model which can be found at the "\_chore\gen__\objects\equipment\unsc\ability_grapple_hook\" directory of your unpacked folder. Once you have navigated here, select the file with the ".render_model" extension and press import. Make sure to disable "import vertex weights" and "(potentially broken) Import Normals"

You will now see that the model you chose has been imported.
![](https://user-images.githubusercontent.com/74399067/206868308-dd53579d-7989-415f-b820-4f10c54d3fdc.gif)

## Fixing Up Imports
### Duplicates/LODs
For stuff like multiple duplicate models, shadow cast models and LODs, you can simply delete them from the viewport.

![](https://user-images.githubusercontent.com/74399067/206869011-d9ae2e5b-fb07-4de0-8c86-981b216687c2.gif)

### UV Flipping
To use the unpacked textures, you will need to flip the UVs of your model. For this, select all your models and press TAB to go into edit mode. Now navigate to the UV editing tab, and on the UV Panel click on "UV" and mirror on the Y axis.


![](https://user-images.githubusercontent.com/74399067/206869188-59ec0083-79fa-40c5-b28f-f34d23b1d3ed.gif)

### Weighted Normals
As the current tools for Infinite cannot extract normal data, we need to use the Weighted Normals modifier to have Blender "guess" the vertex normal data required to have proper shading on our imported models.

For this, you first need to merge by distance on your models, which is possible by going into editing mode with TAB, pressing F3 and searching for "Merge By Distance". After this, go out of edit mode and right click and press "Shade Auto Smooth". And lastly, add the "Weighted Normals" modifier to every model you have with "Face Area and Angle" as the Weighting Mode.

![](https://user-images.githubusercontent.com/74399067/206869497-de1a545a-13cf-4001-9951-7884ef4d5ec2.gif)
![](https://user-images.githubusercontent.com/74399067/206869502-adc95987-9516-41fc-add6-bc48c87448cf.gif)

## Extracting Coatings

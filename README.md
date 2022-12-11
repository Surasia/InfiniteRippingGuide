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
To actually extract models or any data from the game, we need to uncompress it. For this, download HaloInfiniteModuleUnpacker and extract it to a directory. Open "unpacker.py" in Python's IDLE or any other text editor. Now scroll to the bottom of the .py file, where you will see ```unpack_path``` and ```deploy_path```.

> For ```unpack_path``` enter any directory of your choice which has more than 50GBs of space. It is recommended to have it close to the root of your drive.

> For ```deploy_path```, navigate to your Halo Infinite install and copy the path for the ```deploy``` folder.

**Important: Make sure you have use forward slashes (/) and have no backwards slashes present (\\).**

After you've entered the directories, you can now run the script. In IDLE, you can use the Run > Run Module option, or manually run it using cmd ```py unpacker.py```. You should now see the modules slowly listing their file amounts and extracting themselves to the given unpack path.

![](https://user-images.githubusercontent.com/74399067/206862389-6b20ca1f-7579-41ad-a7ad-cd8753d5f356.png)

## Extracting Textures
For texture extraction, we need to use HaloInfiniteMOdelExtractor. Download it and extract it to a directory of your choice. Now open the bitmap_to_dds.py file and again scroll to the bottom of the file. Here, you will see three variables to edit.

> For ```unpack_directory``` use the ```unpack_path``` from the previous step.

> For ```directory``` you can specify a folder to extract in your unpack path, however I recommend just entering ```f"{unpack_directory}"``` which will extract everything in your unpack path.

> For ```out_path```, you can enter any directory you want, however for ease sake I recommend using ```unpack_path``` again.

After you've entered the directories, you can now run the script. In IDLE, you can use the Run > Run Module option, or manually run it using cmd ```py bitmap_to_dds.py```. You should now see textures being extracted and .dds files appearing in the directories listed.

![](https://user-images.githubusercontent.com/74399067/206863140-564ac3ba-d506-45f0-81ca-30e15ba45eb9.png)

## Converting DDS to PNG
While DDS files are good for compression in games, the limited support of it outside of engines can cause issues, especially with Blender. For this, we can convert our files to PNG or TGA using XNConvert, which can batch thousands of files quickly. 

To convert your textures, simply open XNConvert and drag a folder from your unpack directory into it, go to output, select "Delete Original", enable "Use Multiple CPU Cores" with the maximum amount of threads, and set "Format" as PNG.

In this example, I used "elite" from the ```\__chore\pc__\objects\characters``` folder and dragged it into XnConvert.
![](https://user-images.githubusercontent.com/74399067/206863613-c79ebffc-fc6e-4fa2-8c43-a3c830a145db.gif)

## Importing Models 
For this step, you will need Blender and the blender-halo-infinite addon by Coreforge. To install the addon, go to Edit, Preferences, Add-ons and then select the zip you downloaded. You do not need to unzip the file for this step.

![](https://user-images.githubusercontent.com/74399067/206867790-e1e0439e-1f34-4a0b-9cf9-bada0ff8be2c.gif)

Now, in blender, go to File, import and select "Halo Infinite rendermodel". Now, using the explorer in blender, navigate to your unpack folder. Models are most commonly found in the ```\__chore\gen__\``` directory. Here, go into the folder which has the model that you want to import. 

For this example, I used the Grapple Shot model which can be found at the ```\__chore\gen__\objects\equipment\unsc\ability_grapple_hook\``` directory of your unpack folder. Once you have navigated here, select the file with the ```.render_model``` extension and press import. Make sure to disable "import vertex weights" and "(potentially broken) Import Normals"

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

## Setting up HaloInfiniteResearch

To extract coatings, we need HaloInfiniteResearch by Urium86. Download and unzip the "develop" branch to any directory you want. Here, go to ```/configs/config.py``` and open it in any text editor like notepad. Here, you will need to change a few variables.

> For ```BASE_UNPACKED_PATH```, you can use ```unpack_path``` from HIMU.

> For ```EXPORT_JSON```, ```EXPORT_SHADERS``` and ```INFOS_PATH``` use any directory you want, as this will just be a general directory where coatings get extracted to.

> For ```SPARTAN_STYLE_PATH``` use the directory you imported the model with, in my case, ```G:\\HaloInfiniteUnpack\\__chore\\gen__\\objects\\equipment\\unsc\\ability_grapple_hook\\```. This is where ```.materialstyles``` files are usually found.

**Important: Make sure you use double backwards slashes ```\\``` instead of forward slashes or single backwards slashes.**

![](https://user-images.githubusercontent.com/74399067/206900272-dc2f671b-bd95-4581-b508-8086bea04513.png)

## Exporting Coatings

Coatings in Infinite come in tags called "materialpallete" and are categorized per model as "materialstyles". They include information about swatches, which are tileable textures and other variables that make up a zone.

For this step, we need to navigate back to the main directory of HaloInfiniteResearch, and open ```exports\\run_coating_export.py``` in a text editor of your choice. In this file, you will need to edit a few things.

> Delete ```spartan_style``` from the ```'*spartan_style{ct}.materialstyles'``` definition.

> Add the snippet of code below to the top of the file
```
import sys
import os
lib_path = os.path.abspath(os.path.join(os.path.dirname(__file__), '../'))
sys.path.append(lib_path)
```
> Comment Out ```coat_file_name = dict_core[path.stem] + '____' + parse_mwsy.json_base['name']``` and instead add ```coat_file_name = parse_mwsy.json_base['name']``` above or below it.

At the end, the top of your file should look like this. You can now run it.

![](https://user-images.githubusercontent.com/74399067/206901077-0599fcf9-061d-4ace-8f92-d742757bf049.png)

### Troubleshooting with Coating Export

#### "FileNotFoundError: [Errno 2]"
For this error, the solution is very simple. Go to the directory listed, and create the file or folders. You can do this by just creating an empty .txt and and then renaming it to the file listed, such as ```ability_grapple_hook_default.json``` in my case.

#### "Module Not Found"
For this error, you will need to install different pip modules using command prompt. Ensure that you have python added to PATH [https://realpython.com/add-python-to-path/]

After this, open command prompt and type ```pip install [MODULENAME]```. For example, with the "sympy" module, we need to type ```pip install sympy``` and press enter. The only exception to this is with PIL in our file, where you have to type ```pip install pillow```.

## Converting JSONs to Python Files

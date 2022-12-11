# Halo Infinite Model Ripping Guide

## Required Software
- [Blender](https://www.blender.org/download/)
    - [blender-halo-infinite](https://github.com/Coreforge/blender-halo-infinite) 
    - [Halo Infinite Modular Shader](https://cdn.discordapp.com/attachments/1035019724444160081/1035019728445505656/HIMS_2.7.blend)
- [HaloInfiniteModuleUnpacker](https://github.com/Surasia/HaloInfiniteModuleUnpacker)
- [HaloInfiniteModelExtractor](https://github.com/MontagueM/HaloInfiniteModelExtractor)
- [Firefox](https://www.mozilla.org/en-US/firefox/new/)
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

### "Fixing" Normals 
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

For this step, we need to navigate back to the main directory of HaloInfiniteResearch, and open ```exporters\\run_coating_export.py``` in a text editor of your choice. In this file, you will need to edit a few things.

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

![](https://user-images.githubusercontent.com/74399067/206901578-19785ece-4fc9-416d-802a-e35230d4ed85.png)

### Troubleshooting with Coating Export

#### "FileNotFoundError: [Errno 2]"
For this error, the solution is very simple. Go to the directory listed, and create the file or folders. You can do this by just creating an empty .txt and and then renaming it to the file listed, such as ```ability_grapple_hook_default.json``` in my case.

#### "Module Not Found"
For this error, you will need to install different pip modules using command prompt. Ensure that you have python added to PATH [https://realpython.com/add-python-to-path/]

After this, open command prompt and type ```pip install [MODULENAME]```. For example, with the "sympy" module, we need to type ```pip install sympy``` and press enter. The only exception to this is with PIL in our file, where you have to type ```pip install pillow```.

## Converting JSONs to Python Files

To use the exported JSON, we need to convert them to usable python files for Blender. For this, we can use InfiniteCoatingTool by BIOS (Or specifically, my version of it). Download it and extract it to a directory of your choice. Once you have, go into ```Resources\cache.ini``` and open it in notepad. Here, you will see two variables to edit.

> For ```detailMaps```, use the ```__chore\pc__``` in your unpack path. This is where all your textures are kept.

> For ```output```, you can select any folder of your choosing, however I prefer having it inside the CoatingTool directory.

Now, for the final conversion, go back into the root directory of CoatingTool, and open a command prompt in that directory. You can do this by typing "cmd" into the path tab.

![](https://user-images.githubusercontent.com/74399067/206902029-a17c2eab-6949-431b-bc97-4e16d4cbbec9.gif)

In command prompt, now type in ```infinite-coating-tool.exe -i [PATH TO JSON] -n [COATINGNAME]```, and press enter. It will now process your coating into python files.

In my case, this is ```infinite-coating-tool.exe -i G:\CoatingExports\coating\olympus_spartan_grapple_hook_default.json -n olympus_spartan_grapple```

![](https://user-images.githubusercontent.com/74399067/206902311-ab4a8a87-9a34-4319-a859-28b3d0b13f9c.gif)

### Troubleshooting CoatingTool

#### "Infinite_Coating_Tool.UnknownMaterialException"
To fix this error, you will need to replace the Unknown Material in the JSON such as ```cvw_1_layered_alpha``` with ```cvw_7_layered``` in Notepad or any other text editor with the "Replace" or "Find And Replace" function.

#### "System.ArgumentException: An item with the same key has already been added."
For this error, search for the key from the error such as ```8EB26F13```in Notepad, then delete the first occurence of it.

#### "System.ArgumentException: Index Out Of Range."

*Note: This error requires a bit of JSON experience to fix, but I've tried to simplify the overall process.*

This happens when a region has no layers associated with it. To fix this, open the JSON by dragging it into Firefox. Go to the "Raw Data" section and press pretty print. Press Ctrl + A and copy everything which you have selected into notepad. 

Now, navigate to the bottom parts of the file, and search for a "region" with no "layers". Once you have found it, delete starting from after  ```},``` to the other ```},```. 

![](https://user-images.githubusercontent.com/74399067/206915455-a206b678-4f65-4a64-bc74-950d5f8c1d56.png)


## Finding Regions For Materials

Every material in Infinite has special parameters to show where certain coating regions should go to. To find these, we need to open the game itself and Infinite Runtime Tag Viewer, which is a mod tool for Infinite.

**This will not get you banned from Online play, and does not affect others in Online matches.**

When you have Infinite open, launch a map where you know the asset exists in. In my case, for the grapple hook, it can be found directly in the main menu. In IRTV, press "Load" and wait until all tags are loaded. You can now search for the material for your model.

For the grapple hook, the only material present is ```olympus_spartan_grapple_hook_default```, so I have searched for it in IRTV. You can see the materials in a part of your model in Blender using the Material Properties menu.

![](https://user-images.githubusercontent.com/74399067/206903692-05adfe15-42af-45b5-99e4-b31f213c2c5d.png)

In IRTV, after you've found opened the tag, scroll down and open the "style info" menu and look for the "region name". This is a hash which will tell us what script to use when importing our models. 

**Do note that at some times this step is not necessary and the python files will have human-readable names such as "default", however it is good to ensure that you are using the proper files.**

![](https://user-images.githubusercontent.com/74399067/206903813-293ff041-d32e-4757-a2c7-511283930f62.png)

## Importing Coatings into Blender

### Part 1: Running the Python Script
Back in Blender, open the "Scripting" tab and open the python file with the "region name" which you found in the last step. You should now see a big python file inside the tab.

Inside the file, you'll have to edit ```ArmorRegion``` to be ```torso```. You can leave ArmorRegionName as is.

![](https://user-images.githubusercontent.com/74399067/206907482-dc02b18a-5c26-4480-bbd0-cbd8fd85e3db.png)

You can now run the file. If you get any "Index Out Of Range" or "Expected Tuple instead of Float" errors, just press the run button again.

![](https://user-images.githubusercontent.com/74399067/206907591-c3266ab3-187e-451a-b4b4-09d5d729a18e.gif)

### Part 2: Basic Shader Setup

If the script has run, you can move onto the "Shading" tab. You will see that your object is black and has a new material assigned. Copy all the nodes, switch to the old material, delete the nodes there, and paste the nodes you copied.

![](https://user-images.githubusercontent.com/74399067/206907804-88852e80-a700-44ec-809a-f22ea9fea1eb.gif)

After you're done with this, you will have to switch to the new shader. Download Halo Infinite Modular Shader from the "Required Software" section, and Append the nodegroups of the main shader and "Enamel_Smooth".

![](https://user-images.githubusercontent.com/74399067/206908108-99d89ae7-b4e3-4b85-805c-c4882e7f3136.gif)

Now, you'll have to replace the 2.2 shader with the 2.7 one, which is as easy as clicking the icon next to the shader and selecting "Halo Infinite Shader 2.7". I also recommend pulling the shader up a bit to match up with how it was, which you can do by selecting the shader, pressing G and Y, then typing 134.

![](https://user-images.githubusercontent.com/74399067/206908365-2a7b6798-9e12-4aba-ab55-868596c67ce3.gif)

Finally, you will need to add the actual mask textures themselves. Textures are found in the ```\__chore\pc__\``` directory, at the same subdirectory as your models.

As an example for the grapple hook: 
- The model is found at ```__chore\gen__\objects\equipment\unsc\ability_grapple_hook\```
- The textures are found at ```__chore\pc__\objects\equipment\unsc\ability_grapple_hook\```

You can import textures by simply dragging them from Windows Explorer into the Blender nodegraph, and then selecting them from Image Texture nodes. Make sure to insert the proper textures into their spots, such as ASG, Mask0, Mask1 and Normal. If a model is missing the Mask1 texture, use Mask0 instead of it and leave the main ```Mask_0 Texture``` image texture node empty.

**Important: Do not forget to set textures as "Non-Color" inside Blender.**

![](https://user-images.githubusercontent.com/74399067/206908795-1b312912-5d4d-4f4b-989e-9cc5ad950b2c.gif)

When you are done, your model should look fairly done, however there is still much to fix and improve.

![](https://user-images.githubusercontent.com/74399067/206909112-e1c502c4-39e1-4621-99f9-3a991cc56d48.png)

### Part 3: Swatch Fix-Up

Infinite's modular shader system works with different swatches- which are materials with a "GradientMap" which includes a color gradient, and a tileable normal map. You will notice that they are plugged into the main shader.

As the swatches imported with Coating Tool are outdated and have wrong roughness/scaling math inside them, we will need to replace them with the proper math. We can use the "Enamel Smooth" which we imported as a template, as it has the accurate math for the shader.

First, we need to establish which swatch a zone uses. Select a swatch, and press TAB to go inside the nodegroup. There, you will see two textures, the one at the top being the GradientMask, and the bottom one being the Normal.

As an example; 
- ```hum_base_paint_gun_metal_painted_gradientmask{pc}.bitmap.png```
- ```hum_base_paint_gun_metal_painted_normal{pc}.bitmap.png```

are apart of the "gun_metal_painted" swatch. 

![](https://user-images.githubusercontent.com/74399067/206910432-47809e67-b305-4256-a9ee-7c83710afb94.gif)

Now onto actually fixing the swatches. Swap a swatch with Enamel Smooth, duplicate it (or rename it if it's the only instance), rename it with the swatch name from the bitmaps, then switch out the image textures with the ones from the swatch. You can reuse the same nodegroup if the zones have the same swatch.


![](https://user-images.githubusercontent.com/74399067/206910800-830a99c4-dfb1-4d8b-9e3e-00da17a31f97.gif)

![](https://user-images.githubusercontent.com/74399067/206910946-4132c8f6-21d0-4ff5-b39f-63fabab3909c.gif)

**Tip: For easier viewing, you can compact a swatch by pressing "H" while selected.**

![](https://user-images.githubusercontent.com/74399067/206911200-8115b71c-4687-4d31-8f50-a7030a23c95e.gif)

### Part 4: Fixing Zone 2
Due to a bug with CoatingTool, the second zone has the wrong swatch set for it. You can check what swatch it uses with the JSON.

Simply drag your coating JSON into Firefox, and you will see it open in a JSON viewer. Expand ```regionLayers``` and look for the ```region name``` from IRTV. Expand it and go into layers. Finally, expand "1" which is the second zone. You will see the ```swatchID ``` for the zone, which you can look up in the next section.

![](https://user-images.githubusercontent.com/74399067/206911822-88e19dda-0a27-4134-b856-0547cb8cdd7a.png)

Now, to find the swatch used, go to the "swatches" section above and look for the swatch which uses the ```swatchID ``` from the previous step. In my case, the swatch ID is ```E8B4E5A9``` which is the "gun_metal_painted" swatch. You can now change it in Blender as well.

![](https://user-images.githubusercontent.com/74399067/206912013-70539436-def9-49a1-9ce1-75cd5b2ad67a.png)

### Part 5: Fixing the GrimeSwatch

For this step, we will also need to open the JSON file in Firefox. At the very top of the file you will spot ```GrimeSwatch``` with a SwatchID next to it. Like with the Zone2 fix, open up the swatches section and look for the swatch used.

![](https://user-images.githubusercontent.com/74399067/206912242-f084c8e5-5f21-461d-9932-585ba04259c3.png)

In my instance, it is using the "Base Dust 01" swatch, with the listed values. Back in Blender, make sure to enter the proper values into boxes such as 
- "Roughness/Roughness Black/Roughness White" which can be entered into the shader
- "TopColor/MidColor/BotColor" which are R/G/B values (in order) which can be entered into the shader by clicking onto the color boxes.

Any other values such as "ScratchColor" are currently not necessary.

![](https://user-images.githubusercontent.com/74399067/206912513-3b355778-4873-4267-ba4b-e60460e1e984.png)

### Part 6: Fixing the DustSwatch

Some models use an additional zone called "Dust" inside mask1 to add detail to models, such as Chief's campaign model. These are found in the last entry in a regionlayer, and are usually empty with the default swatch being present: ```00000000```.

Using the same steps as Part 5, you can enter the values for Dust just like Grime. However, even if your model has a swatch listed in its last layer, it still depends on the material used (see below). 

**If the "material" inside your RegionLayer has "damage" inside it, such as "cvw_7_layered_damage", it means that it does. If it doesn't, you do not need to bother with this step.**

If your model does in fact use Dust, make sure to enable it on the top of the blender shader by setting "Dust Amount" to 1.

![](https://user-images.githubusercontent.com/74399067/206912842-9d3c2926-a85c-457e-be68-bee4a1458a24.png)
![](https://user-images.githubusercontent.com/74399067/206913166-b113f49e-4fdc-4338-b6dd-1c8e48be981d.png)

### Part 7: Entering Scaling Values

Scaling in Infinite is done using 8 parameters, which can be found in the material and swatch tags in Infinite. For this step, we will need to open IRTV and again navigate to our .material tag. Here, open the "material parameters" tab and switch over to the second (1) entry.

![](https://user-images.githubusercontent.com/74399067/206913682-32da2e28-3a39-4f6f-8010-3be6e788a4ed.gif)

There are 4 values here which you need;
- ```Real``` for "Base Scale X" in Blender
- ```Vector X``` for "Base Scale Y" in Blender
- ```Vector Y``` for "Material Transform X" in Blender
- ```Vector Z``` for "Material Transform Y" in Blender

For the remaining values, we'll need to open the ```.materialswatch``` tags in IRTV. Search for the swatch used in a zone, such "hum_plastic_painted" and open up the tag.

![](https://user-images.githubusercontent.com/74399067/206914056-f0c3698e-ec5d-4584-8356-7d9727b64de7.png)


There are 4 values here which you need;
- ```ColorAndRoughnessTextureTransform X``` for "Gradient Scale X"
- ```ColorAndRoughnessTextureTransform Y``` for "Gradient Scale Y"
- ```NormalTextureTransform X``` for "Gradient Scale X"
- ```NormalTextureTransform Y``` for "Gradient Scale Y"

![](https://user-images.githubusercontent.com/74399067/206914769-673bafbb-d65b-4835-9fb3-234a730cd6a6.png)

## Congrats! Your model is now properly imported.

![](https://cdn.discordapp.com/attachments/1047606773290373120/1047606774502531202/GrappleShot.png)

## Common Issues and Solutions

### Is it possible to import a rig and weights attached to a model?
Currently, there is no rig/weight support for imports done with the Blender addon. There is work being done however, with Urium's tool managing to extract rigs with partial weights, but it is far from done as of now.


### When I try to import from the python file, it gives me a "File Not Found" error. What can I do?

Some textures in Infinite are packed into a single .bitmap file, which HaloInfiniteModelExtractor cannot extract. For these textures specifically, you can use [Mohawk](https://github.com/Twigzie/Fantality-Infinite-Mohawk) which can extract them. Don't forget to rename them and put them into their proper directories once they are extracted.


### Some of my mormal Maps are corrupted- how can I fix this?
As HIME doesn't support some DirectX Normal types, it can cause corrupted normal maps to appear. To properly extract these textures, you need [RawTex](https://forum.xentax.com/viewtopic.php?f=18&t=16461) [[Mirror]](https://cdn.discordapp.com/attachments/1004426111633080380/1020822059477127258/Rawtex.rar). 

Simply drag the biggest .bitmap tag file (such as ```.bitmap[3_bitmap_resource_handle.chunk3]```) into Rawtex, change the scaling according to the file and select BC5S as the texture format. For the 0xOFFSET, start with "337" and slowly iterate until you get a proper normal map.

Scaling values for bitmaps are:
- ```.bitmap[3_bitmap_resource_handle.chunk3]``` -> 2048x2048
- ```.bitmap[2_bitmap_resource_handle.chunk2]``` -> 1024x1024
- ```.bitmap[1_bitmap_resource_handle.chunk1]``` -> 512x512
- ```.bitmap[0_bitmap_resource_handle.chunk0]``` -> 256x256

### I'm getting a "struct.error: unpack requires a buffer of 4 bytes" error. How can I fix this?
This means that the .materialstyle you are trying to extract is from campaign, and requires [a different version of HaloInfiniteResearch](https://github.com/urium1186/HaloInfiniteResearch/tree/f65119545ed75d2c4338e8dcd99231b8f671eb40). 

The same setup needs to be done as the regular one, with a single additional edit made to the ```\tag_reader\readers\materialpalette.py``` file. Open the file in a text editor, and comment the 36th line. The image below should be how it looks like at the end. You can now save and run the coating export again.

![](https://user-images.githubusercontent.com/74399067/206918918-4e3a6531-86ea-455d-ab98-5d08517b2ea9.png)


### I don't want to/can't add Python to PATH. How can I use pip?
Navigate to your python install folder. This is normally found in ```C:\Users\USER\AppData\Local\Programs\Python\Python37"```. Go inside the scripts folder here, and open a command prompt by typing "cmd" into the path menu. You can now enter the pip commands here.


## Still have issues/questions? Feel free to submit them on the "Issues" page of this repository.

# Credits
## My sincere thanks to:
- Coreforge for his amazing Blender addon and support of the Halo ripping community. His tools have helped a ton in creating this guide.
- Average Goblin/Goat/Trap Enthusiast for his work on Halo Infinite Modular Shader and research of the Halo Infinite shader system. And also being the biggest Mark IV enthusiast alive. 
- Montague Moran for creating HIMU/HIME, which have been essential in the development of other tools.
- Gamergotten/Krevil/Z-15 for their contributions to the Halo Infinite modding community. IRTV has given really insightful info such as the scaling values in this guide, and is an invaluable tool for anyone interested in modding Infinite.
- BIOS for creating Infinite Coating Tool. It has saved me at least a couple hundred hours of work, with more to come :D
- TheJudSub for creating the template python script and iterating over the shader, creating the foundation for the porting process.
- Plastered_Crab for creating the Halo Archive and C.R.A.B. (Central Research Archive Bureau) where almost all of the research into Infinite has taken place, contributing to the python script and supporting the community for years <3
- Urium86 for creating HaloInfiniteResearch and allowing for much more data from tags to be extracted. He has been working really hard for the last few months on this project even while being on a limited time schedule. 
    - You can support him at: http://shorturl.at/ab037 and https://www.patreon.com/fromb1t0life.
- Deskclaw for teaching me how to use Rawtex.





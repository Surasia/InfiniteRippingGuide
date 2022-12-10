# Exporting Models from Halo Infinite

## Required Software
- [Blender](https://www.blender.org/download/)
    - [blender-halo-infinite](https://github.com/Coreforge/blender-halo-infinite) 
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
![3ad711da59519b1eb83ef6988d0bba40](https://user-images.githubusercontent.com/74399067/206863613-c79ebffc-fc6e-4fa2-8c43-a3c830a145db.gif)

## Importing Models 


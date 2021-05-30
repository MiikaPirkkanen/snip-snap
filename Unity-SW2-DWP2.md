# How to integrate Stylized water 2 with Dynamic Water Physics 2 in Unity

It so happens that there is no simple guide on how to integrate aforementioned assets at this time so I ended up writing one as this seems to be asked quite alot. 
In this guide we are integrating [Stylized Water 2](https://assetstore.unity.com/packages/vfx/shaders/stylized-water-2-170386) water shader asset with 
[Dynamic Water Physics 2](https://assetstore.unity.com/packages/tools/physics/dynamic-water-physics-2-147990) water simulation tool. When we are done we have an ocean 
rendered with Stylized Water 2 shader with physically accurate waves.

I'm using Unity 2020.1.17f1.4949 with Universal Render Pipeline, Stylized Water 2 (v. 1.0.9) and Dynamic Water Physics 2 (v.2.4.2). Other versions should also work 
but you should check that from their respected websites. These were the latest versions of the assets at the time of writing.

Both of these assets use Assembly Definitions (.asmdef -files) and they are also used in this guide.

## Setting up Dynamic Water Physics 2
To start you should make sure you can get the Dynamic Water Physics 2 to work with FlatWaterDataProvider. Create a new project, add DWP2 to the project via Unity 
package manager and follow this guide from their documentation page: http://dynamicwaterphysics.com/doku.php/QuickStart

## Stylized Water Data Provider script
Open the Unity pacakge manager again and add SW2 to your project. Now you can delete the water plane created in the previous step as we are going to use SW2 to draw 
the surface of water. Navigate to the following folder in the project panel `Assets/StylizedWater2/Runtime`. Here you can find a text file called 
`StylizedWaterDataProvider.cs.txt`. Convert this file to a C#-script by clicking the right mouse button inside the folder and selecting `Create -> C# Script` and name 
the script `StylizedWaterDataProvider.cs`. Copy the contents of the .txt -file to the newly created .cs -file. This script implements the DWP2's `WaterDataProvider` 
interface to let the water simulation know about the water height.

## Link the DWP2 assembly definition
The StylizedWaterDataProvider script has to be aware of this interface and this will be done via Assembly Definitions. Select the `sc.stylizedwater2.runtime` file 
from the `Runtime` folder and find `Assembly Definition References` section from the inspector. Click the plus icon to add a new row and then click the circle icon on 
the row to open the assembly definition selector. Select `NWH.DWP2` assembly reference asset and now stylized water has access to the DWP2's `WaterDataProvider` 
interface. Click "Apply" when prompted if you want to update the assembly references.

## Creating the Stylized Water
Navigate to the `Prefabs` folder under Stylized Water 2 asset and drag and drop the water prefab you wish to use to the scene. Once in the scene attach 
`StylizedWaterDataProvider.cs` script to the water game object. All that is left is to set the parameters of the scripts via inspector.

#### `StylizedWaterDataProvider.cs` parameters
|Parameter           | Value                                                                                     |
|--------------------|-------------------------------------------------------------------------------------------|
|`Water Mat`         | Select the material your prefab is using from the folder `Assets/StylizedWater2/Materials`|
|`Water level source`| Select `Fixed value`                                                                      |
|`Water Level`       | Input the y-coordinate of your water objects world position                               |

## Making waves
Now is a good time to play with the wave parameters in your stylized water object. Select the object from the scene and modify the StylizedWater materials parameters
to your liking. Water physics now react to the wave parameters you come up with.

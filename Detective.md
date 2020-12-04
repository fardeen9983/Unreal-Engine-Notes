# Getting The Detective Environment

## Brainstorming
1. Brainstorm notes off of a project brief
2. Using notes to derive the visual reference
3. Creating sketches and maps based on references
4. Narrowing a reference down to key images

### Project Brief
A brief is a simple document that outlines the summary of project ideas. For this project, we will use the following Brief
> Using the inspiration of detective thrillers, we will create a scene using UE that is self-contained but has depth and story. The camera setup will be the First Person and the gameplay style will be adventure mystery, which will be influenced by the scene set dressing, lighting, and audio. Leverage existing creative content for inspiration such as Mindhunter, True Detective and L.A.Noire

### Brainstorming Notes
* Where is this taking place geographically? New York city
* What is this space or object? Private office and dwelling
* What is this space or object used for? Detective's office
* Who uses this space or object? Burnt out the detective in his mid 40's
* What is the person doing currently? Trying to solve a kidnapping
* When is the scene taking place in time? 1990's
* When was this space or object built originally? 1890's
* What time of day it is? Dusk
* What is the weather like? Overcast

### Reference
Make sketches or collect material for inspiration like
* Structures 
* Exterior/interior
* Props

After deciding on the visual reference of the scene we are going to working on the actual layout of the scene and create the Map

### Mood Board
After going through all the references we set up a mood board which is built to establish our desired art style, subject matter, and structure

## Project conventions
1. Naming conventions for files
2. How to setup folder for the scene
3. Using an asset list to drive production and time estimates

### Naming conventions
* Static meshes - SM prefix, ex: SM_Bookcase
* T prefix for textures and suffixes are to drive the texture type
  * _D for Diffuse [base color]
  * _N for Normal
  * _M for Masks (occlusion, roughness, metallic)
  * Example - T_Bookcase_D
* Material - MI

### Folder setup
Content -> Assets -> Textures -> Structures -> Texture file

### Asset list
Contains a table with the following columns
* File Name
* Placement
* Folder
* Material Name
* Texture Name (Multiple)

## Creating a new project
Unreal Launcher -> Game -> Select Template (First Person) -> Project Settings (Blueprint, Max Quality, RTX disabled, Desktop, No Starter Content) -> Select Path and Project name

## Scenes
1. a Basic overview of the interface
2. Using the World outliner and organizing it
3. Removing starter content from the scene
4. Setting up content browser folders

### Cleanup Steps
1. Delete everything in the scene other than the player and the floor
2. Create a new folder - Static Mesh
3. Selecting an object and pressing `Ctrl + B` (Browse to Asset) highlights all the assets it uses in the Content Browser
4. Delete the previous Geometry folder and move the meshes folder in it to the root
5. Add New -> Create Two folders -> Materials and Textures

## Blueprint
Has a
1. Construction Script
2. Event Graph
3. Viewport

Remove crosshair
1. Edit the FirstPersionHUD Blueprint
2. Hold down Alt + Press Left click on any  active pins to break their branch 
3. Compile and Save - Green tick means everything goes great

Remove Hands and guns from the camera
1. Edit the FirstPersonCharacter BP
2. Goto Viewpoint Tab
3. Select each of the guns and hand objects from the viewport either by clicking on them or selecting from the Components panel on the left (much like the World Outliner of a scene)
4. Go to their Rendering property in the Details panel and untick visibly
5. Compile and Save

Remove the projectile shooting
1. Goto the FirstPersonCharacter Blueprint
2. Select the Event Graph tab and select SpawnProjectile sheet
3. Disable both input branches - InputActionFire and InputTouch
4. Compile and save

Make the character slow down
1. Go to the Components of the FirstPersonCharacter BP
2. Select CharacterMovoment (inherited)
3. In the Details panel go to general settings
4. Drop the Max acceleration from 2048 to 500
5. Go Walking section and change ground friction from 8.0 to 2.0 and set the walking speed to 500
6.  

## Block Out space
1. Create a Blockout space - A mapped environment created with simple blocks only - in any designer software
2. Create pivotal points for objects or surfaces to join in place
3. Never work without a scale character
4. Create an FBX export
5. Save that as an asset in Unreal project's Mesh folder
6. Go to the Mesh folder Content browser and import the new FBX model
7. For importing a static mesh, keep a note of 3 things
   1. Auto-generate collision - Disabled
   2. Generate Lightmap UVs - Enabled
   3. Material Import method - Do not create material
   4. Right-click on the new import and save
   5. Add the model to the scene and align the floor to it by selecting different perspectives
8. Hold down L and Left click to place a point light anywhere in the scene
9. Adjust the structure - like if it is too tall or lengthy


### Breaking into pieces
It is a best practice to break down the block out model or static meshes into smaller manageable pieces to reduce the loading time. FOr this, we select and export specific layers of the model from the modeling software. IN this way the blackout model becomes a kind of like a skeleton placeholder for the rest of the model and is separated. Next in Maya by keeping the Blockout layer as a reference we select one by one the other layers and export them as separate assets to create our asset list. For example, at one point we will export all 4 walls together with reference to the blackout block

It is important to understand that this is not the final model. What we are doing is simply separating the block parts of the model. But this gives the advantage of updating a specific part of the scene.

## Adding collisions
1. Blocking Volume 
   
    These are invisible blocks of space we can use as obstacles. They already have collision enable d so we can mix them with passthrough walls to make them collide 

2. Editing the asset's collision property

    If we select the asset in the content browser window popups with a collision tab. The best option among them is Auto Convex COllision which will try best to cover the asset in the collider mesh. There are properties like hull count and vertices, increasing which will increase the complexity of the collision mesh

3. Creating your collisions in Maya
   
    In Maya, we can loosely wrap the object in primitive spaces. The naming convention for the cubes will be as follows - `UCX_ASSETNAME_0X`. Here UCX stands for Unreal Collision

### Tips
1. Using blocking volumes for flat floors when you start a scene
2. The auto-create collision options in the editor are great for a quick pass but not very accurate and can be costly as good memory-wise
3. Creating custom collision for your asset while in the 3D package allows more control and usually less memory
4. Make sure to use the UCX prefix for custom collision
5. Add numbered suffix for more than one asset used in the collision (_01)

## Materials
1. Go to materials folder
2. Right-click and select material - This creates a default material
3. Rename it to M_Props (M_ prefix for material)
4. CLicking on it opens the material editor
5. Hold T + Left click to add a texture sample - Create three such textures
6. Mappings :
   1. Texture 1: RGB to Base color
   2. Texture 2:
      1. R to Ambient Occulsion
      2. G to Roughness
      3. B to Metallics
   3. Texture 3: RGB to Normal
7. To remove errors on the Texture samples
   1. Click on any texture sample
   2. Go to details panel in lower left and select the texture dropdown
   3. In view options enable Show Engine Content
   4. From the texture lists select 
      1. 127grey for Texture samples 1 and 2
      2. BaseFlatternNormalMap for sample \
8. Conver each of the textures to parameter. Give them a name - Diffuse, Mask, Normal
9. Save and exit from the material inspector
10. Right-clickck on the material and create a material instance
11. Rename the material instance with MI prefix and the speicif name of the object it will be applied on like MI_Chair
12. Similarly create material instance for props and structure and spearate them out into folders - Props and Structure
13. We use the Materials as base for creating all other Prop and Strucutre Material Instance

## Importing textures
1. Softwares like substance painter are used for created textures for assets
2. Export settings - Unreal Engine (Packed), Targa, 8 bits
3. 3 textures are exported - Diffuse, Mask, Normal
4. Based on the prefix (T) and suffix (D, M, N) the imports will be compressed differently - how many channels they will be using (Occlusion, metallic, roughness)
   1. Diffuse - Default 3
   2. Mask - no sRGB
   3. Normal - Normalmap
5. Similarly create folders for Props and Structure

>**Note**
>Power of 2 is helpful in file compression when creating textures. It also helps keep files standardized in terms of sizing

## Applying textures and materials
1. Click on the material to open the material inspector
2. For each of the parameter for DMN we have created in the materials, drag and drop the respective texture and select the option that says "use selected asset from the content browser"
3. After doing this for all the 3 of the texture samples, we return to the mesh we want to apply the material on
4. A mesh can have multiple materials as we can see in the mesh inspector's details panel. 
5. But for now we just drag and drop the material we have modified onto the mesh and voila the exact textures are applied on it

## Ligthting
### Types
* Directional - Day/Night
* Point - Expensive. Not used much
* Spot
* Rect
* Sky - Ambient light

We can select these options from the modes option in the left panel. It is also important to note that all materials will automatically reflect or obstruct light as per their material. 

### Directional light 
To make the room more darker we can obstruct the light spread by enclosing the scene inside a shell - a large object with smaller focused openings for light - placed as such that it will cover the entire scene from outside

### Point light
These are more expensive to bake and do remember to disable casting shadows. These are generally avoided and used only when in blockout phase

### Spot Light 
Has a conical light exposure. Can be used for light sources that throw light in a conical fashion. We can control both the inner and the outer cone angles for a better contorl on light diffusion

### Rect light
For omnidirectional lighting of lamps and screens

To add the glow of light from objects supposedly emitting light we have to create a separate material with a 3 channel texture (RGB). Give it a glow color (0.9, 0.81, 0.68) and add it to a multiply sheet (multiply by 20) and attach it to the new material's Emissive color. Finally add this material to the object's channel which needs to be glowing

You can mix and match different types of light together to match the source's said behavior. Also to lighten up an object we can press Ctrl + L + left click on that object. This will create a point light there with the same color as that on the clicked object. Good way to fake global illumination

Another trick when Lighting a sign is to scroll down in the Light object's property upto the Light Profiles > IES Texture and select whichever looks appropriate.

Other than the individual light object properties we can also control lighting on the entire scene from the world settings - like ambient occlusion

LigtMassImportanceVolume is a Light based property which creates a boundary for light in the scene and based on it's properties we can control the number of bounces on it. On the other hand for opening like windows we place LightMassPortals over them to create a bleeding effect over the eges

Reflection captures help drive the roughness of the metallic channels of the material. There are two types - Box and Sphere (default) Reflection capture - available in the Visual Effects panel in the modes

Just drag and drop it in the center of the room to be lit or near objects or points in the scene where we need more reflection, and tweak the radius so it almost fits the room. For additional Rendering settings goto:

Edit -> Project Settings -> Rendering -> Reflections

and change the reflection capture resolution


### LightMaps
Lightmaps shouldn't make overlapping UV as they will lead to weird lighting effects like black spots. Also the lightmap resolution should be kept at reasonable value (~256). Pressinbg Alt + Num0 brinks the Lightmap density. Anyhing deviating towards red is more complex. ideal color is green. To bring down or up the complexity, just tweak the lightmap resolution

## Post-processing
Post-processing refers to adding some additional effects to the scene after baking to add more features like atmospheric fog, Bloom, etc. The first person template already comes occupied with the Atmospheric Fog and PostProcessVolume option in the world outliner. If not present already we can get them from Modes -> Visual Effects


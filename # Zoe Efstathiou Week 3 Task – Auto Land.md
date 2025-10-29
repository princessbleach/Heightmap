# Zoe Efstathiou Week 3 Task – Auto Landscape Materials
**Unit:** Technical Art (Level 5 Games Development)  
---


### 1. Height-Based Blending System  
**Technical Requirements:**  
- Implement **automatic texture blending** based on world height/elevation
- Create smooth transitions between at least **3 height zones** (e.g., valley floor, hillside, mountain peak)
- Use **LandscapeLayerBlend** nodes with height-driven alpha masks
- Include **transition falloff controls** for artistic adjustment
- Demonstrate **snow region**, **grass region** and **mountain region** transitions
\
![a](https://github.com/princessbleach/Heightmap/blob/main/landscapelayers.png?raw=true)


![blend](https://github.com/princessbleach/Heightmap/blob/main/blend.png?raw=true)

![height](https://github.com/princessbleach/Heightmap/blob/main/step1.png?raw=true)



**Guiding Questions:**
- How do you prevent harsh transitions while maintaining distinct biome characteristics?
- What height ranges work best for different landscape scales?
- How does height blending interact with other blending systems?

---

### 2. Slope-Based Blending System  

I then added a slope-based blending system that ensured the rock material would appear on sloped and steep areas of the lanscape whilst also blending in seemlessly. 


**Technical Requirements:**  
- Implement **automatic texture blending** based on surface angle/slope
- Create distinct materials for **flat surfaces** (grass, sand) vs **steep surfaces** (rock, cliff faces)
- Use **LandscapeLayerWeight** with slope calculations
- Include **slope threshold controls** with smooth falloff




Standard UE heightmaps aren't suited to handle overhangs and complex geometry as they only store one vertical value per point. The material would have to use world-space normals instead of height. This means rock could then be applied to surfaces facing downwards.
To create realistic transitions; under 20 degrees should be vegetation and soily surfaces, 20 - 45 degrees should be where rock appears to due erosion, above 45 degrees is where rock or snow should be fully covering the area. However, this depends from project to project. Slope blending imitates real whethering of rock and soil as in life there are not harsh, blocky transitions between surfaces. By following a set of rules, it can act similarly to nature itself rather than having to rely on the artist to paint based off their jurisdition. 

---

### 3. Foliage Type Integration and Generation 

I began by creating a Static Mesh Foliage asset for the grass and added this into a Procedural Foliage Spawner. I then placed the PFS into the scene to cover a small area of the lanscape. When first using the foliage spawner for my grass, I encountered multiple issues; at first, the grass spawned sparcely and did not change even when increasing initial seed density. After troubleshooting, I enabled the grow and spawn in shade variables which fixed the problem. I then found (as seen in gif below) that the further grass meshes were darker until walked up to. I deleted the mesh's lod3 which seemed to fix the issue. 

![badgrass](https://github.com/princessbleach/Heightmap/blob/main/badgrass.gif?raw=true)

I then created another SMF for the flowers. I decreased the initial seed density and, to create a more realistic growth pattern, I  decreased the average spread distance to create natural clusters of flowers. 

![foliage](https://github.com/princessbleach/Heightmap/blob/main/foliage.png?raw=true)

I then created my third foliage type: trees. I decreased the initial seed density to a value much lower than the other foliage and also decreased the num steps to ensure all trees were similar sizes. 

![nograss](https://github.com/princessbleach/Heightmap/blob/main/nograss.png?raw=true)

Upon adding trees to the PFS, I encountered an issue where my grass dissapeared. I was able to fix this by adjusting the overlap priority parameters for each foliage type. I ensured the grass had a higher priority than the other foliage to ensure it would spawn. I then did the same for the flowers. 

![three](https://github.com/princessbleach/Heightmap/blob/main/grassflowertree.png?raw=true)

For increased realism, I wanted to ensure grass and flowers only spawned within a certain height range and only on grassy parts of the lanscape. I also wanted trees to not spawn on slopes and stones to spawn densely on the rocky areas of the lanscape. Within the placement area of the SMFs I specified the min and max height range for each foliage type. I also specified the lanscape layers to be included and exluded. I created two stone SMFs, one for a lower height range and one for heigher. I decreased the initial seed density when the rocks were in the lower height boundary and increased seed density for the heigher boundary SMF. 

![placemet](https://github.com/princessbleach/Heightmap/blob/main/rocks.png?raw=true)


These placement parameters ensure realism within the lanscape as the foliage can follow real enviromental rules; trees growing on flat areas, flowers not growing on snow or under shade etc. 


When spawning foliage I found the engine to be unresponsive and slow, especially when using the resimulate function. I found that using lower quality meshes and decreasing num steps for each foliage helped to decrease any performance issues, as well as decreasing the PFS area and only increasing the initial seed density by small increments. However, the engine still remained slow.  When doing foliage in the future I will optimise my engine beforehand to ensure smoother/quicker workflow. 



---

#### Bibliography
ChatGPT 5.0 was used for the following: ideation and suggestions to meet the brief. find non academic sources and documentation on the web. modifying and enhancing README. MD


Epic Games (n.d.) *Fab Marketplace assets* [Game assets]. Unreal Engine Fab. Available at: https://www.fab.com .


How to Auto Adapt Landscape Material to Height in Unreal Engine 5 (Tutorial) (2024) Directed by EZ Unreal. At: https://www.youtube.com/watch?v=6qG7Gf-pMtY 
 
Procedural Foliage Tool in Unreal Engine | Unreal Engine 5.6 Documentation | Epic Developer Community (s.d.) At: https://dev.epicgames.com/documentation/en-us/unreal-engine/procedural-foliage-tool-in-unreal-engine .


Save hours! Procedural Foliage in Unreal Engine 5 - Photoreal Landscape Tutorial (2023) Directed by Aziel Arts. At: https://youtu.be/JpbWi95Bz20?si=IeDXlxJJZJghZOPo .


Epic Games (2024) Landscape Material Expressions and World-Space Normals in Unreal Engine 5.6 Documentation. Available at: https://dev.epicgames.com/documentation .



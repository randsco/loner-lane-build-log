**Situation**: The buildings at Loner Lane have been lost and we are taking the opportunity to rebuild using new techniques.
**Motivation**: Using unique textures across different surfaces on each building results in high texture memory usage causing slower loading times, higher texture trashing rates, and lag. Only using tiled textures introduces repetition across large surfaces with small details and lacks contrast around edges and crevasses. Edges on objects in real life are rarely perfectly square and adding bevels on the mesh itself adds mesh complexity. Outward facing edges often have additional wear compared to surfaces, and crevasses can collect dirt.

**Solution**: By using a combination of [trim sheets](https://www.patreon.com/posts/lets-talk-about-94999921) and reusable tilable textures, a compromise is reached striking a balance between the amount of texture memory consumed and contrast at creases and edges.

**Method**: First, [procedural edge wear](https://i.gyazo.com/e78d1e845c387820324e9e12ddaa5599.png) is added to materials to create the contrast between the centre of faces vs the periphery. Next, the material albedo is baked down to a scaled trim [sheet/texture atlas hybrid](https://i.gyazo.com/614cb7e24bc22a7f16e03af8bc904a4b.jpg) including the respective occlusion roughness metallic and normal maps. Then, the [faces on the mesh are unwrapped](https://i.gyazo.com/78bd0bc241caf52273c9c1b2a2751ddb.jpg) using the [hotspotting](https://www.artstation.com/artwork/oA55G4) method assigned to their respective materials. Lastly the LOD for the model is created along with the physics shell.**Results**: The [final result](https://i.gyazo.com/b702d1e101761b0332a582a1d0cbefb5.jpg) is an 11x11 metre building at 8 LI mapped to a single 1024x1024 texture.

**Discussion**: The LOD model might appear to lack detail but the decision to have it this way was a compromise based on a few considerations.
The building is to be placed within a courtyard surrounded by other tall buildings and is unlikely to be the focal point when viewed from afar. As long as the silhouette remains I thought that would be an acceptable compromise for achieving a significantly lower land impact. 
The pinnacle at the top is a separate object and linked afterwards because including it would increase the building's bounding box dimensions by 2 metres in each direction as object radius is always a cube in SL which has implications on each LOD, so it [follows that the land impact will also be negatively impacted](https://community.secondlife.com/forums/topic/59414-download-weight-and-size-some-graphs/) by a factor much greater than would necessitate including the pinnacle. In my tests, the pinnacle would add another 4 land impact to the total building bringing it to a total of 12 LI wheras keeping them separate results in a land impact accounting of building 8 LI + pinnacle 0.5 LI = 8.5 LI which is significantly less. The conclusion here is that especially on high density meshes, detail should be evenly distributed throughout the mesh and as close to a cube bounding box as possible to achieve the lowest possible land impact. Outliers should be split into separate meshes.
**Next Steps**: I would include more variation on trim dimensions as many are stretched beyond what looks good. I would then use a separate high-resolution texture for the brick as the texel density is too low currently relative to the trims and looks blurry. Additonally, having the brick adjacent to the floorboard texture on the UV layout prevents tiling in the horizontal direction.

Tools Used: 
- [Blender 4 LTS](https://www.blender.org/download/lts/4-5/)
- [DreamUV Blender Plugin](https://github.com/leukbaars/DreamUV)

Texture Sources:
- [Texturelabs (for dirt and wear masks)](https://texturelabs.org/)
- [Blenderkit](https://www.blenderkit.com/)
- [Polyhaven](https://polyhaven.com/)
- [CGBookcase](https://www.cgbookcase.com/)

References:
 - [Second Life Community - Download Weight and Size: Some Graphs by Drongle McMahon](https://community.secondlife.com/forums/topic/59414-download-weight-and-size-some-graphs/)
- [Hotspot Materials: And You Can Too! by Dave Face](https://www.artstation.com/artwork/oA55G4)
- [The Last of Us: Part I...Trim Pipeline by Matthew Trevelyan Johns: Principal Environment Artist - Naughty Dog Studios](https://trevelyan.artstation.com/projects/qQGK6y)

More Case Studies:
- [Felyx's Guide to Trim Sheets by Felyx McGarry](https://www.artstation.com/blogs/jennifermcgarry/yd4Q/jenns-guide-to-trim-sheets)
- [Handpainted vs Single Trim Sheet Workflow: Old Wooden Church by Bohdan Ozheredov](https://www.artstation.com/artwork/1NJbz2)
- [Feudal Japan Trimsheet Overview by Keegan Keene](https://www.artstation.com/artwork/dOymdx)

Model Analysis and Guided Workflows
- [(3 hours) Using Trim Sheets to Build Complicated Assets Quickly on gametextures.com by Keegan Keene](https://www.youtube.com/watch?v=qODD-79i5_4)
- [Trim Texture Tutorial Series by Polygon Academy](https://www.youtube.com/playlist?list=PLBi3xvwvY3dk09fNSd7jrnEscXS_6_1p2)
- [Intro to Trims Series by Claudius D'Souza](https://www.youtube.com/playlist?list=PLU74dDTYexO5ap_Ko9stC-RZs5Pw1cJOi)

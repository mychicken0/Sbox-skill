 about

Terrain Materials

A T errain Material is an Asset that defines a set of PBR textures, physics surfaces, detail meshes and

other properties that the T errain uses to render.

Because they are Assets you can easily reuse them on multiple T errains in different Scenes easily, transfer

them between projects, or use them from the cloud.

These are similar but different to standard Materials because T errain uses specialized shaders for rendering

to deliver performant landscape rendering with LOD support and material blending.

The first T errain Material you apply to a T errain automatically becomes the base layer, and spreads over

the whole landscape. You can then paint areas with other T errain Materials blending them together.

Creating T errain Materials

To create a new T errain Material, select your T errain GameObject and look at the Inspector, under T errain

Materials press New Terrain Material… Pick a save location and it will be automatically added to your

T errain Material list.

You can also create a T errain Material that isn't automatically associated with a T errain, by rick-clicking the

Asset Browser and selecting New Asset → New T errain Material…

Adding T errain Materials

Existing T errain Material assets can be dragged from the Asset Browser into the T errain Material list - or

onto the T errain itself.

T errain Materials can be found on the cloud by clicking the Browse… button, or filtering @cloud ext:tmat .

T here is a limit of 4 T errain Materials currently, this is planned to be resolved.

T errain Material Properties

Painting T errain Materials

The first material is applied across the entire T errain by default. You can paint subsequent T errain Materials

using the Paint T exture tool and selecting the T errain Material in the list in the inspector.

Updated 21 Jul 2024
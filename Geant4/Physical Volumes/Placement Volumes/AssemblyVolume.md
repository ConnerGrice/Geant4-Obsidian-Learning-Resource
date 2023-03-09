This is a class that is a type of [[PhysicalVolume]]. It allows the user to create a group of volumes, then copy and move them all around together. Its concrete class is the [`G4AssemblyVolume`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/volumes/include/G4AssemblyVolume.hh).

Unlike the [[Repeated Volumes]], the assembly volume is filled is multiple placement volumes and acts as an envelope for all the daughter volumes. Once the logical daughter volumes are places, its role is over and the final structure is comprised on independent copies.

## Reasons for usage

- For more complex structures that can't be described with [[PVReplica]] or [[PVParameterised]].
- Structures that contain many different shapes
- Very dense structures that can't use the mother volume

## Usage
```cpp
//Create the assembly object
G4AssemblyVolume* assembly = new G4AssemblyVolume();

//Add logical volumes to the assembly
assembly->AddPlacedVolume(exampleLogicalVolume, examplePosition,exampleRotation);
... //Add all other logical volumes inside assembly using coordinates with respect to the assembly volume

//Do something to the assembly coordinates to generate a new one
for (int i = 0; i < exampleRange; i++){
	assemblyRotation = ...//New rotation of repeated assembly
	assemblyTranslation = ..//New position of repeated assembly

	//Generate a new assembly in a new position that contains the same geometry
	assembly->MakeImprint(logicalWorld,assemblyTranslation,assemblyRotation);
}
```
When these new assemblies are generated, the independent physical volumes are given an automatic name. This is the format:
- `av_WWW_impr_XXX_YYY_ZZZ`
The different parts of the name are as follows:
- `WWW` - Assembly volume instance number.
- `XXX` - Assembly volume imprint number.
- `YYY` - Name of the placed logical volume in assembly.
- `ZZZ` - Index of the associated logical volume.

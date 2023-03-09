This is the standard and most simple [[PhysicalVolume]]. It is represented by the [`G4PVPlacement`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/volumes/include/G4PVPlacement.hh) class.

It is simple in the fact that when the user creates one of these objects, only a single volume will be placed in the simulation world.

Like all other physical volumes, this object must take a [[LogicalVolume]] in order for it to know the properties of the volume it is placing.

There are 2 different contractors for this class. However, they are very similar but one uses a `G4Transform3D` object and the other uses a `G4RotationMatrix` for the rotation relevant to its mother volume and a `G4ThreeVector` for the translation. Once can generate a `G4Transform3D` by using a rotation matrix and vector.

```cpp
G4PVPlacement(G4RotationMatrix* pRot,
	 const G4ThreeVector& tlate,
	 const G4String& pName,
	 G4LogicalVolume* pLogical,
	 G4PhysicalVolume* pMother,
	 G4bool pMany,
	 G4int pCopyNo,
	 G4bool pSurfChk = false);
```
The attributes are as follows:
- `pRot` - The rotation of the volume relative to the mother volume
- `tlate` - The position vector of the volume relative to the mother volume
- `pName` - The name of the volume
- `pLogical` - The logical volume that represents the volume being placed
- `pMother` - The mother volume that the represented volume is inside of
- `pMany` - **Note in use**, should allow for volume overlapping
- `pCopNo` - A unique ID number given to the volume
- `pSurkChk` - Activates checks for overlapping with existing volumes
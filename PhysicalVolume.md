The physical volume is the type of volume that specifies the location the geometry will be inside of its mother volume. It is the last layer of the system.

There are many different types of physical volume that serve different purposes, here are a few:

- **[`G4PVPlacement`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/volumes/include/G4PVPlacement.hh)**: The simplest type of physical volume that will just place the shape at the given location with a given rotation.
- **[`G4PVReplica`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/volumes/include/G4PVReplica.hh)**: This type is used to generate multiple copies of a given logical volume along a singular axis (linear or circular).
- **[`G4PVDivision`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/divisions/include/G4PVDivision.hh)**: This is very similar to `G4PVReplica`, however, it is more limited. The mother volume must be completely filled and there can't be any gaps between daughters.
- **[`G4PVParameterised`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/volumes/include/G4PVParameterised.hh)**: This is the most complex type of physical volume. It is also used to generate multiple of the same shape however, the user can specify exactly how this is done using a class derived from the `G4VPVParameterisation` base class.

An example declaration continuing from [[LogicalVolume]]:
```cpp
//rot -> A rotation matrix defining the shapes rotation, using G4RotationMatrix*
//pos -> A position vector using G4ThreeVector()
//logicalExample -> The logical volume this physical volume represents
//logicalWorld -> The logical volume of the mother volume
//many -> A bool specifing if the volume is meant to overlap over other volumes
//copyNo -> A unique number identifer
//overlap -> A bool specifying if the program should check for any overlap
physicalExample = new G4PVPlacement(rot,pos,logicalExample,"Example_p",logicalWorld,many,copyNo,overlap);
```


The logical volumes are what are used to define the logical response that volume has to other aspects of Geant4 and is represented by the [`G4LogicalVolume`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/management/include/G4LogicalVolume.hh) class. Some of the aspects defined within the logical volume are:

- **[Materials](Material.md)**: These are parameters used within Geant4 to determine how different particles will respond while travelling through the geometry.
- **[Sensitive Detectors](SensitiveDetector.md)**: If a logical volume is designated as a sensitive detector, that means that that piece of geometry will react when hit by a particle and record some values.
- **Visualizer Attributes**: These are options given to the volume that determine how the volume will look when the visualizer is running. Whether it will be wireframe or solid for example.

An example declaration continuing from [[SolidVolume]] and [[Material]]:
```cpp
//solidExample -> solid volume already given
//exampleMaterial -> Material object already given
logicalExample = new G4LogicalVolume(solidExample,exampleMaterial,"Example_l")
```

Once the logical volume is defined, a [[PhysicalVolume]] can then be defined in order to place the geometry into the simulation.
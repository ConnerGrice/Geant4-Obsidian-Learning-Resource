The solid volumes are the lowest level of volume within Geant4. This is where the shape is defined by specifying the dimensions. There are many different types of sold volumes that ask for different dimensions:
- [`G4Box`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/solids/CSG/include/G4Box.hh) 
- [`G4Tubs`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/solids/CSG/include/G4Tubs.hh)
- [`G4Sphere`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/solids/CSG/include/G4Sphere.hh)
All of these solid volumes use the [`G4CSGSolid`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/solids/CSG/include/G4CSGSolid.hh) base class.

An example declaration:
```cpp
//x,y,z are the half side lengths of the box
solidExample = new G4Box("Example_s",x,y,z);
```

Once the solid volume is defined, the [[LogicalVolume]] is the next step. 
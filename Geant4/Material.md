Materials are objects given to a [[LogicalVolume]] the will determine the behaviour that different particles will exhibit while traveling through them. There are a few ways to define materials.

## Using NIST
This method uses the collection of already defined materials using the `G4NistManager`. The list of defined materials can be found [here](https://geant4-userdoc.web.cern.ch/UsersGuides/ForApplicationDeveloper/html/Appendix/materialNames.html).

A simple example of getting a material is as follows:
```cpp
//Declare the mist manager
G4NistManager* nist = G4NistManager::Instance();

//Get the desired material (Silicon in this example)
exampleMaterial = nist->FindOrBuildMaterial("G4_Si");
```

Composite materials are also available.

This material can them be put into a logical volume.

## Custom Material

This method involves given different parameters for a custom material. Geant4 has its own material object called [`G4Material`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/materials/include/G4Material.hh). The types of parameters that would need to be defined are:
- Atomic number
- Mass of a mole
- Density
- State (solid/gas)
- Base material (if a composite material)

An example:
```cpp
//Defines a material that matches that of gold
G4Material* exampleMaterial = new G4Material("Gold",79.,196.96654*g/mol,19.300*g/cm3);
```

```ad-note
The units given in the code example are defined using the [`G4SystemsOfUnits.hh`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/global/management/include/G4SystemOfUnits.hh) header file. These are just renames of [CLHEPs already defined units](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/externals/clhep/include/CLHEP/Units/SystemOfUnits.h).
```

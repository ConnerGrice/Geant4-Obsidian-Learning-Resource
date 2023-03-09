This class is where the 3D geometry is defined as well as any [sensitive detectors](SensitiveDetector.md) or fields. 

This class must be a child class of the [`G4VUserDetectorConstuction`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/run/include/G4VUserDetectorConstruction.hh) abstract class/interface.

In order for the geometry to be constructed, the user created class, in this case `ExampleDetectorConstruction` must make use of the abstract virtual method [[Construct()]]. Therefore, the basic detector header file would look like this:

```CPP TI:"ExampleDetecorConstruction.hh"
class ExampleDetectorConstruction: public G4VUserDetectorConstuction {

public:
	//Default constructor
	ExampleDetectorConstruction();
	//Deconstrictor
	~ExampleDetectorConstruction();

public:
	//Place to define the geometry to ge generated
	G4VPhysicalVolume* Constuct();
	void ConstructSDandField();
};
```

[[ConstructSDandField()]] is not a mandatory method, however, it is used when defining the [[SensitiveDetector]] and the different fields within the simulation space.

As seen, the `Constuct()` method will return an object called `G4VPhysicalVolume`. The volume it is asking for the called the `world`. In Geant4, all geometric objects must be placed within some other object (the mother). The `world` is the only object that can stand on its own, it is at the top of the hierarchy. All other shapes must reside inside the `world`, however, shapes can also be placed inside other shapes inside the `world`. 

The basic geometry is defined using 3 different types of volumes. The:
- [[SolidVolume]]
- [[LogicalVolume]]
- [[PhysicalVolume]]

A volume must also be given a [[Material]] in order for Geant4 to understand how this geometry will react to particles within the simulation.

Below is an example of a simple `Constuct()` method in which an empty world is generated.

```CPP TI:"ExampleDetectorConstuction.cpp"
G4VPhysicalVolume* ExampleDetectorConstruction::Constuct(){

	//Defines the material the world will be made of (Vacuum)
	G4NistManager* nist = G4NistManager::Instance();
	WorldMat = nist->FindOrBuildMaterial("G4_Galactic");

	//Defines each type of volume the world will be
	solidWorld = new G4Box("World",500*cm,500*cm,500*cm);
	logicalWorld = new G4LogicalVolume(solidWorld,worldMat,"World");
	physicalWorld = new G4PVPlacement(0,G4ThreeVector(0,0,0),logicalWorld,"World",0,false,0,true);

	return physicalWorld;
}
```

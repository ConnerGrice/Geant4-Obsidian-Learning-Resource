This method is what defines what will be in the simulation space. It returns the `world` volume, and therefore, since all other volumes must be inside of a mother volume, with the `world` as the apex, will contain all other volumes in the space.

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
Where `worldMat` is the material object that will determine how the world interacts with particles. This method of creation is shown in [[Material]]. 
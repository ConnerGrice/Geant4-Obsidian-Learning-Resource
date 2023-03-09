This method is used to assign which [[LogicalVolume]] will be set as a [[SensitiveDetector]]. It is also used to define the [[Field]] within the simulation area.

## Assigning Sensitive Detectors
An example of adding the sensitive detector property to a logical volume is below. This method involves first declaring a sensitive detector object, then using the `G4SDManager` to add the sensitive detector object to the manager, then finally, using the `SetSensitiveDetector()` method provided by the `G4VUserDetectorConstruction` base class. This will continue from the [[SensitiveDetector]] example.

```cpp 
void ExampleDetectorConstruction::ConstructSDandField(){
	//Generate SD object
	auto sensDetObject = new ExampleSD("ExampleSD","ExampleCollection");
	
	//Add it to the manager ()
	G4SDManager::GetSDMpointer()->AddNewDetector(sensDetObject);
	SetSensitiveDetector("ExampleLogical",sensDetObject); 
}
```

## Assigning Fields
When assigning fields, the user must make use of the [`G4FieldManager`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/geometry/magneticfield/include/G4FieldManager.hh). This class is created before the [[DetectorConstruction]] is called and is associated with the `world` volume. The example below illustrates how to set a field to the `world` volume. It is a continuation of the example field created in [[Field]]:
```cpp
void ExampleDetectorConstruction::ConstructSDandField(){
	//Define the custom field
	auto magField = new ExampleField();
	
	//Create the field manager variable
	G4FieldManager* globalFieldManager = G4TransportationManager::GetTransportationManager()->GetFieldManager();

	//Set the field in the field manager
	globalFieldManager->SetDetectorField(magField);
}
```
The user can also assign the field to a specific [[LogicalVolume]]. This is done by defining a `G4FieldManager` with a given field, then feeding that field manager into the logical volume.
```cpp
void ExampleDetectorConstruction::ConstructSDandField(){
	//Define the custom field
	auto magField = new ExampleField();
	
	//Assign the field to the field manager
	G4FieldManager* localFieldManager = new G4FieldManager(magField);

	//Assign the field manager to the logical volume
	logicalVolume->SetFieldManager(localFieldManager,true);
}
```
In this example, `logicalVolume` would be an object defined in [[Construct()]] of the type `G4LogicalVolume`. The `true` attribute in the `SetFieldManager()` method tells the program to associate this field with the logical volume and all of its daughter volumes. 
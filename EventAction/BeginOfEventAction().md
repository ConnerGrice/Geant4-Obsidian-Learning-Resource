This method is part of the [[EventAction]] class and it is called when an [[Event]] begins (As primary particles are generated). This method is extremely flexible and the user can utilise this method as they please, however, for the sake of example, this method will be used to get the [[Hit]] collection ID in order for the [[EndOfEventAction()]] method to utilise the complete collection at the end of the event. The sensitive detector manager was used to get this ID because the hits collection is associated with the [[SensitiveDetector]] class, and created in the [[DetectorConstruction]]-[[ConstructSDandField()]] method. 
```cpp
void ExampleEventAction::BeginOfEventAction(const G4Event* anEvent) {
	//Gets the manager that will be used to get collection ID
	auto SDetectorManager = G4SDManager::GetSDMpointer();

	//Checks if collection has already been generated
	if (exampleHitsCollectionID == -1){
		exampleHitsCollectionID = SDManager->GetCollectionID("ExampleCollection"); 
	}
}
```
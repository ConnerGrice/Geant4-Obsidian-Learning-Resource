This method is part of the [[Event]] class and will be called when an event is over (all particles have been popped off the stack). This methods main function could be to process the completed [[Trajectory]] objects or other collections. 

This example will show how this method can be used to get the [[Hit]] collection generated during the event, and get the position where each hit occurred. This will use the [[Hit]] example class methods. It will also continue the example in [[RunAction]], showing how the user would collect positional data into an external file using the `G4AnalysisManager`, also detailed in [[RunAction]], and finally, it will be the end of the example started in [[Digi]] and [[DigitizerModule]] in which digits will be generated using [[Hit]]s collected during an event.
```cpp
void ExampleEventAction::EndOfEventAction(G4Event* anEvent) {
	//Get all the hit collections generated from the event
	auto HCE = anEvent->GetHCofThisEvent();

	//Gets instance for external file managment object
	G4AnalysisManager* manager = G4AnalysisManager::Instance();
	//Initialise collection to be assigned
	ExampleHitsCollection* exampleCollection = nullptr;

	//Check if hit collections exist
	if (HCE) {
		//Gets the hit collection if it exists 
		if (exampleHitsCollectionID != -1) {
			exampleCollection = (ExampleHitsCollection*)(HCE->GetHC(exampleHitsCollectionID));
		}
	}

	G4int numberHits = 0;
	//Checks for collection
	if (exampleCollection) {
		//Gets number of hits inside collection
		numberHits = exampleCollection->entires();

		//Loops through all hits inside collection
		for (G4int i = 0; i<numberHits; i++){
			//Gets position vector of hit
			G4ThreeVector position = (*exampleCollection)[i]->GetPosition();

			//Fill the data into the corresponding rows
			//manager->FillNtupleDColumn(tableID,columnNumber,Data)
			manager->FillNtupleDColumn(0,0,position[0]);
			manager->FillNtupleDColumn(0,1,position[1]);
			manager->FillNtupleDColumn(0,2,position[2]);

			//Add data to the table
			manager->AddNtupleRow(0);
		}
	}

	//Initialise the digit manager
	G4DigiManager* fDM = G4DigiManager::GetDMpointer();
	
	//Get the digitizer module and invoke the digitize method
	ExampleDigitizerModule* digiModule = (ExampleDigitizerModule*)fDM->FindDigitizerModule("ExampleDigitizer");
	digiModule->Digitize();
}
```

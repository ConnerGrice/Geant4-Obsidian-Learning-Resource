This method is called at the start of an event. it takes an object called `G4HCofThisEvent` or _hit Collection of this event_. This method will normally assign a hit collection object to the sensitive detector. This example continues from the [[Hit]] example:
```cpp
void ExampleSD::Initialize(G4HCofThisEvent* hce){
	//Get the collection
	fexampleHitsCollection = new ExampleHitsCollection(SensitiveDetectorName,collectionName[0]);

	//Get the collection ID and add it the this event
	G4int hcID = G4SDManager::GetSDMpointer()->GetCollectionID(fexampleHitsCollection);
	hce->AddHitsCollection(hcID,fexampleHitsCollection);
}
```
In this example, a hit collection is generated using the name of the sensitive detector that was activated. Once the collection is generated, the identifying number is found using the `G4SDManager`. After getting the ID, this hit collection is then added to the specific event that the sensitive detector detected. This allows for multiple collections to be assigned to a single event.
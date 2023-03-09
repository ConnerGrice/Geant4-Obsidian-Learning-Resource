This method is part of the [[StackingAction]] class. It is called whenever the **Urgent** [[Stack]] is empty and there is at least 1 [[Track]] in the **Waiting** [[Stack]]. It is called a _stage_ when this method is called. Its main purpose is to reclassify all the tracks in the **Waiting** stack in order to transfer them over to the **Urgent** stack. Another use for this method is to abort the current [[Event]] is some condition is met. All of these functionalities are done by the `G4StackManager` object.

In this example, the user wants to abort the event if too many particles hit too many sensitive detectors or there has already been 4 _stages_ within the [[Event]]. If this condition is not met, the tracks will be reclassified. This example is a continuation from [[StackingAction]].
```cpp
void ExampleStackingAction::NewStage() {
	//Incriment the event counter
	numberOfStages++;
	
	//NOTE: This method is not defined anywhere and will simply get the hit collection of the current event
	ExampleHitsCollection* collection = GetCollection("ExampleCollection");

	//Gets the total number of hits inside the collection
	G4int numberOfHits = collection->entries();

	//Checks if the number of hits is too high and there has been less than 4 events
	if (numberOfHits > 10 || numberOfStages > 4) {
		//If too high, clear the waiting stack
		stackManager->clear();
		return;
	}

	//If low enough, transfer waiting stack to the urgent stack
	stackManager->ReClassify();
	return;
}
```
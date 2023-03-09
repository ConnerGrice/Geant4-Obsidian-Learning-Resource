This method is part of the [[RunAction]] class. It is called at the start of a [[Run]], e.g. When the first primary particles are generated by the primary generator. 

The example shown will be the user that wants to set up external files in order to collect data throughout all the events. Therefore, at the start of the run the user must open the file that will be filled. This is done using the `G4AnalysisManager`. More info can be found in [[RunAction]].
```cpp
void ExampleRunAction::BeginOfRunAction(const G4Run* aRun) {
	//Creates manager instance and sets it to a ROOT system
	auto manager = G4AnalysisManager::Instance();

	//Opens file
	manager->OpenFile();
}
```
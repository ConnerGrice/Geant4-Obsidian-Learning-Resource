This is a method within the [[RunAction]] class. It will be called at the end of a [[Run]] (When the last [[Event]] is deleted). 

The example shown in [[RunAction]] is that of a user that wants to collect information into an external file. The file structure is generated in the class constructor shown in [[RunAction]], while the file is opened in the [[BeginOfRunAction()]] method. Therefore, once all the data is collected throughout each event using the [[EventAction]] - [[EndOfEventAction()]], the data must then be written into the file system. This will be done in this method and is shown below. This will use the `G4AnalysisManager`, more info can be found in [[RunAction]].
```cpp
void ExampleRunAction::EndOfRunAction(const G4Run* aRun) {
	//Creates manager instance
	G4AnalysisManager* manager = G4AnalysisManager::Instance();

	//Writes data into file
	manager->Write();

	//Closes file as the program ends
	manager->CloseFile();
}
```
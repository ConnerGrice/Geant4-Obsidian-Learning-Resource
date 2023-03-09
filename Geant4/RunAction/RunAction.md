This is the class that a user can create that will define the processes that will take place at the start and end of a [[Run]].

It must be a child class of the [`GUserRunAction`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/run/include/G4UserRunAction.hh) base class. Therefore, the user must implement the abstract methods:
- [[BeginOfRunAction()]]
- [[EndOfRunAction()]]

This class is very flexible and is very case specific to what the user wants their program to do. However, common function is to generate, open and close external files for data collection at the start and end of a run. This is going to be the illustrated example. 

Below is an example header file for the run action:
```cpp
class ExampleRunAction: public G4UserRunAction {
public:
	ExampleRunAction();
	~ExampleRunAction();

public:
	void BeginOfRunAction(const G4Run* aRun) override;
	void EndOfRunAction(const G4Run* aRun) override;
}
```
Since this class is responsible for the creation of the data table that will be used, this needs to be done when the class is created. This is done by utilising the [`G4AnalysisManager`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/analysis/factory/include/G4AnalysisManager.hh), which is just a copy of the [`G4GenericAnalysisManager`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/analysis/factory/include/G4GenericAnalysisManager.hh) class. The file system that will be used in this example is the [ROOT](https://root.cern/) framework. Therefore, a constructor responsible for collecting positional data of hits is shown below.
```cpp
ExampleRunAction::ExampleRunAction() {
	//Create the manager object
	G4AnalysisManager* manager = G4AnalysisManager::Instance();

	//Assign/create a file that will be associated with the manager
	manager->SetFileName("Example_Data.root");

	//Generates table with a name and ID
	manager->CreateNtuple("TableID","TableName");
	//Creates rows inside the table
	manager->CreateNtupleDColumn("x");
	manager->CreateNtupleDColumn("y");
	manager->CreateNtupleDColumn("z");
	...//Generate all columns in table
	//Close table 
	manager->FinishNtuple(0);

	...//Create all other tables
}
```
```ad-note
The data is collected by the [[EventAction]] class in this instance.
```
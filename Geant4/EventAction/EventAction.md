This class is used by the user to extract information about [[Event]]s within their simulations. This class must be a child class of the [`G4UserEventAction`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/event/include/G4UserEventAction.hh) class. Therefore, it must also include the abstract methods:
- [[BeginOfEventAction()]]
- [[EndOfEventAction()]]

A common implementation of this class is to track the total energy deposited by all particles during a simulation. Doing this will be shown in this example and continued in [[SteppingAction]] - [[UserSteppingAction()]]. Another major role of this class is to utilise [[Trajectory]] paths and other collections generated during the event. Finally, this class is also used when the user wants to collect data to be recorded into an external file - See example starting in [[RunAction]]. 

This is an example of a simple header file that contains the utility to sum energy over an entire event:
```cpp
class ExampleEventAction: public G4UserEventAction{
public:
//Constructors
	ExampleEventAction();
	~ExampleEventActin();

public:
	//User impliemented abstract methods
	void BeginOfEventAction(const G4Event* anEvent) override;
	void EndOfEventAction(const G4Event* anEvent) override;

private:
	//Methods used for summing energy over an entire event
	void AddEnergyDeposit(G4double energyDeposition) { Edep += energyDeposition; };
	//Total deposited energy
	G4double Edep;
	G4int exampleHitsCollectionID;
	
};
```

Since the example being shown will track the total energy deposition throughout the entire event, the `Edep` variable must be reset at the start of every event. The `exampleHitsCollectionID` must also be declared. This is done on creation of this class. Following the digit example in [[Digi]] and [[DigitizerModule]], the constructor must also utilise `G4DigiManager` to define the [[DigitizerModule]] that will be used in the member methods of this class. An example of this is below:
```cpp
ExampleEventAction::ExampleEventAction(): Edep(0),exampleHitsCollectionID(-1){

	//Define digitizer
	ExampleDigitizerModule* digiModule = new ExampleDigitizerModule("ExampleDigitizer");
	
	//Add to the manager
	G4DigiManager::GetDMpointer()->AddNewModule(digiModule);

}
```
**NOTE**: `exampleHitsCollectionID` is set to -1 in order to check if the [[SensitiveDetector]] assigned to it in the [[ConstructSDandField()]] method actually had any hits (generated a hits collection).
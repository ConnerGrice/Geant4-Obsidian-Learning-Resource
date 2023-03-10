A sensitive detector is a tag you can give to a [[LogicalVolume]] that tells Geant4 that that volume is going to be recording data during a run.

In order to define how the data will be recorded a child class of [`G4VSensitiveDetector`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/digits_hits/detector/include/G4VSensitiveDetector.hh) must be created. There are 3 virtual methods that can be used when defining the sensitive detector, as well as the default constructor:

1. [[Initialize()]] - Called at the start of an event
2. [[ProcessHits()]] - Used for data collection using [[Hit]] objects
3. EndOfEvent() - Called at the end of an event, can be used for record data

An example of a simple sensitive detector header file is below:
```cpp
class ExampleSD : public G4VSensitiveDetector{
public:
	//Default constructor
	//name -> Name of sensitive detector
	//collection -> Name of hits collection
	ExampleSD(G4String name, G4String collection);
	~ExampleSD();

	void Initialize(G4HCofThisEvent* hce); //Run at start of event
	G4bool ProcessHits(G4Step* aStep,G4TouchableHistory*); //
	void EndOfEvent(G4HCofThisEvent*); //Run at end of event
private:
	//Hit collection used in other methods
	ExampleHitsCollection* fexmapleHitsCollection;

};
```

## Default Constructor
If a hits collection is being used, then this must be declared in the constructor. Meaning that when a SD is created, it must be linked to some sort of hits collection to start collecting data. This is a simple example of that:
```cpp
//Create an instance using the base class, giving the SD a name, and creating the empty hit collections variable
ExampleSD::ExampleSD(G4String name, G4String collection): G4VSensitiveDetector(name),fexampleHitsCollection(0){
	//This variable is given by the base class
	collectionName.insert(collection);
}
```

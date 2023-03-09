This class is used to to extract the information from the hit collections and convert them into digit collections. This class must be a child class of the [`G4VDigitizerModule`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/readout/include/G4VDigitizerModule.hh) base class. Therefore, the user must define the abstract method, [[Digitize()]]. This method is not called by Geant4, therefore, the user must invoke this method manually. The most natural place to do this would be in the [[EventAction]]-[[EndOfEventAction()]] because by this time, the hit collections will be complete.

This class must be invoked within the [[EventAction]] therefor example will continue from there, just as it is a continuation from the [[Digi]] example. 

The example header file is as follows:
```cpp
class ExampleDigitizerModule: public G4VDigitizerModule {
public:
	ExampleDigitizerModule(G4String name);
	~ExampleDigitizerModule();

public:
	void Digitize() override;
}
```
Since the digitizer is the class that creates the collection, similarly as to how the [[SensitiveDetector]] class creates the [[Hit]] collection, this must be done in the creation of the class. The variable `name` represents the detector module that is connected to the collections and is managed by the base class. This is an example of a basic constructor:
```cpp
ExampleDigitizerModule::ExampleDigitizerModule(G4String name):
	G4VDigitizerModule(name) {
	//Create collection
	collectionName.puch_back("ExampleDigitCollection");
}
```
This is a child class of the [`G4VHit`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/digits_hits/hits/include/G4VHit.hh) base class, used to store data about particle interactions between themselves and a [[SensitiveDetector]]. In essence, they are a grouping of variables with corresponding `set` and `get` methods.

Within the hit class, one can define a [`G4THitsCollection`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/digits_hits/hits/include/G4THitsCollection.hh) object, this is an array of hits that is filled during an event. An example of its use can be found in [[Initialize()]]

A basic hit class is shown below:
```cpp
class ExampleHit: public G4VHit{
public:
	ExampleHit();
	~ExampleHit();
	
	inline void SetPosition(G4ThreeVector pos) {fpos = pos;};
	inline G4ThreeVector GetPosition() {return fpos;};

private:
	G4ThreeVector fpos;

};

//This defines the hit collection object that will contain a list of examples hits
typedef G4THitsCollection<ExampleHit> ExampleHitsCollection;
```

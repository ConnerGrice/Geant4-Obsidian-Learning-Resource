This is a class the the user can define and will tell the program how to process data at the start and the end of a [[Track]], which is a snapshot of a particle as it moves through the simulation.

One of the important uses of the tracking action is to for a collection of tracks to form a [[Trajectory]]. This is done by utilising the [`G4TrackingManager`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/tracking/include/G4TrackingManager.hh) given in the example below. 

The tracking action is a user created child class of [`G4UserTrackingAction`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/tracking/include/G4UserTrackingAction.hh). Therefore, the user must define 2 abstract methods:
1. [[PreUserTrackingAction()]] - Will run when a particle is generated
2. [[PostUserTrackingAction()]] - Will run when a particle is deleted, detailed in [[Track]].

The basic tracking action header file is below:
```cpp
class ExampleTrackingAction: public G4UserTrackingAction{
public:
	//Constructors
	ExampleTrackingAction();
	~ExampleTrackingAction();

public:
	//User defined methods
	void PreUserTrackingAction(const G4Track* aTrack);
	void PostUserTrackingAction(const G4Track* aTrack);

private:
	//Tracking manager used to store into a trajectory
	G4TrackingManager* mTrackingManager;
};
```
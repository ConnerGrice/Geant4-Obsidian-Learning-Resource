This method is part of [[TrackingAction]] and will be called at the start of each tracking event.

One of the main uses for this method is to collect tracks into a list of [`G4TrajectoryPoint`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/tracking/include/G4TrajectoryPoint.hh) objects into a [[Trajectory]] object. This is done by using the [`G4TrackingManager`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/tracking/include/G4TrackingManager.hh) class. This is shown below:
```cpp
void ExampleTrackingAction::PreUserTrackingAction(const G4Track* aTrack){
	//Check if the particle is a primary particle
	if (aTrack->GetParentID() == 0){
		//Start the collection tracking
		mTrackingManger->SetStoreTrajectory(1);
	}
	else{
		//Do not start collecting the tracking
		mTrackingManager->SetStoreTrajectory(0);
	}
}
```
`mTrackingManager` is defined in the header file in [[TrackingAction]].

```ad-warning
The user should be careful about tracking all particles (including secondary particles) due to the fact that this may take up lots of memory.
```
However, if the user is using their own custom [[Trajectory]], the `G4TrackingManager` is also used. This is a snippet on how that would be used:
```cpp
mTrackingManager->SetTrajectory(new ExampleTrajectory());
```

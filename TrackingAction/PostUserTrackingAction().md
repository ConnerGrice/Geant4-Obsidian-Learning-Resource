This method is part of the [[TrackingAction]] class and is called at the end of a tracking event. There could be many different ways the user could use this class. For instance, the position of the particles when it eventually runs out of kinetic energy (since this is one of the reasons the track will stop and this method will be called.).
```cpp
void ExampleTrackingAction::PostUserTrackingAction(G4Track* aTrack){
	//Checks if the track was stopped because the particle lost all of its kinetic energy
	if (aTrack->GetKineticEnergy() != 0){return;}

	//Gets the position of the particle using the track
	position = aTrack->GetPosition();

	//Method to record the data into some external file
	RecordData(position);
}
```
Note that `RecordData()` is not defined anywhere and is used for illustration purposes only. 
This method is part of the [[StackingAction]] class. It is called whenever a new [[Track]] is to be added to a stack. It can also be called by the `G4StackManager` by the user by invoking the `Reclassify()` method. The main function of this method is to assign the track to a specific stack. This is useful for prioritising track processing.

This method returns a [`G4ClassificationOfNewTrack`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/event/include/G4ClassificationOfNewTrack.hh) enumerator. This represents the stack that the track will be assigned to. The classifications are:
1. `fUrgent` - Push onto the **Urgent** [[Stack]].
2. `fWaiting` - Push onto the **Waiting** [[Stack]].
3. `fPostpone` - Push to the **PostponeToNextEvent** [[Stack]].
4. `fKill` - Delete [[Track]] all together.

A common use for this method may be to force the program to process only the primary particles before going through all the secondary particles. This will be shown in this example, by assigning secondary particles to the **Waiting** stack, as well as illustrating how the user could delete particles that are _electrons_ (Any particle type can be used).
```cpp
G4ClassificationOfNewTrack ExampleStackingAction::ClassifyNewTrack(const G4Track* aTrack) {
	
	//Gets the type of particle
	G4ParticleDefinition* particleType = aTrack->GetDefinition();
	
	//Get is the particle was primary or not
	//0 = Primary
	//0 < Secondary
	//0 > From last event (Postpone stack)
	G4int parentID = aTrack->GetParentID();

	//Checks that particle is not an electron
	if (particleType != G4Electron::ElectronDefinition()) {
		//Checks that particle is a secondary particle
		if (parentID > 0) {
			//Push to waiting stack if secondary particle that ISNT an electron
			return fWaiting;
		}
		//Push to urgent stack if primary particle that ISNT an electron 
		return fUrgent;
	}
	//Delete all particles that ARE electrons
	return fKill;
}
```
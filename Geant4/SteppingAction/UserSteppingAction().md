This is a method that is part of the [[SteppingAction]] class. It will be called at the end of a [[Step]]. Since an [[Event]] is a collection of data generated from steps, a common usage of this method is to calculate values throughout the [[Event]].

This is an example of how a user would go about calculating the total energy deposited the simulation world.
```cpp
void ExampleSteppingAction::UserSteppingAction(const G4Step* aStep){

	//Gets the energy deposited by the particle at the end of the step
	G4double energyDeposition = aStep->GetTotalEnergyDeposit();

	//Add this value to a value that is tracked over an event (multiple steps)
	//This method is defined in [[EventAction]]
	mEventAction->AddEnergyDeposit(energyDeposition);
}
```
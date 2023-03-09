This method is part of the [[ActionInitialization]] class and it is used to bring all the user created action classes together. It will follow a simple but similar pattern between programs. This is an example of the method being used to connect all the types of action classes available:
```cpp
void ExampleActionInitialization::Build() const{
	SetUserAction(new ExamplePrimaryGeneratorAction);

	ExampleRunAction* run = new ExampleRunAction();
	SetUserAction(run);

	ExampleEventAction* event = new ExampleEventAction();
	SetUserAction(event);

	ExampleStackingAction* stacking = new ExampleStackingAction();
	SetUserAction(stacking);

	ExampleTrackingAction* tracking = new ExampleTrackingAction();
	SetUserAction(tracking);

	ExampleSteppingAction* stepping = new ExampleSteppingAction();
	SetUserAction(stepping);
}
```
The `SetUserAction()` is a method provided by the `G4VUserActionInitialization` base class.
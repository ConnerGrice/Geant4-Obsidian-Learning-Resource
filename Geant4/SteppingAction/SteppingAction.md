This class is for defining the actions that will take place at the end of each [[Step]] of the simulation. It must be a child class of the [`G4UserSteppingAction`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/tracking/include/G4UserSteppingAction.hh) and it only requires a single abstract method to function:
- [[UserSteppingAction()]]

A common use of the stepping action class is to keep track of the energy deposited into a material by a particle. For this, it must be linked to the [[EventAction]] since this is the class that can hold information over a number of steps, unlike the stepping action. The example below is the header file for this common use case. It will continue in [[EventAction]]:
```cpp
class ExampleSteppingAction: public G4UserSteppingAction{
public:
	ExampleSteppingAction(ExampleEventAction* eventAction);
	~ExampleSteppingAction();

public:
	void UserSteppingAction(const G4Step* aStep);

private:
	ExampleEventAction* mEventAction
}
```
If the user wants to collect information throughout the [[Event]] using [[Step]]s, the [[EventAction]] class must be created when the stepping action is created in order to link them. This is an example of the default constructor if you user want to link with the [[EventAction]]:
```cpp
//Once the object is created, the event action that is passed in is assigned to a variable.
ExampleSteppingAction::ExampleSteppingAction(ExampleEventAction* eventAction): mEventAction(eventAction){

}
```
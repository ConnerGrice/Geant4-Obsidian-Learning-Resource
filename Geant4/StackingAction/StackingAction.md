This is the class that is responsible for the actions that are taken during the processing for the [[Track]] objects during an [[Event]] from the [[Stack]]. It must be a child class of the [`G4UserStackingAction`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/event/include/G4UserStackingAction.hh) base class. This means that the user must implement 3 abstract classes:

1. [[ClassifyNewTrack()]] - Called by the [`G4StackManager`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/event/include/G4StackManager.hh) every time a new [[Track]] is stored and is used to define which stack the track will be stored in.
2. [[NewStage()]] - Called by the `G4StackManger` when the **Urgent** stack is empty and [[Track]] objects in the **Waiting** stack are transferred over.
3. [[PrepareNewEvent()]] - Called when ever the **Urgent** and **Waiting** stacks are empty and a new [[Event]] is about to start.

This action class is useful for prioritising specific tracks and particles for processing in order to save memory or computation time. 

In the example continuing in [[NewStage()]], the user wants to make sure that less than 4 _stages_ have taken place. This means defining the stage counter in the header file. This is an example of the header file:
```cpp
class ExampleStackingAction: public G4UserStackingAction {
public:
	ExampleStackingAction();
	~ExampleStackingAction();

public:
	G4ClassificationOfNewTrack ClassifyNewTrack(const G4Track* aTrack) override;
	void NewStage() override;
	void PrepareNewEvent() override;

private:
	G4int numberOfStages;
}
```

Since the _stages_ counter must be declared on created on the stacking action, it is defined in the constructor as follows:
```cpp
ExampleStackingAction::ExampleStackingAction(): numberOfStages(0){

}
```
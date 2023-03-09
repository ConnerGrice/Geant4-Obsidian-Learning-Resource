This method is part of the [[StackingAction]] class. It is called at the start of a new [[Event]], when the **Urgent** and **Waiting** stacks are empty. However, there may be [[Track]] objects inside the **PostponeToNextEvent** [[Stack]]. If tracks are inside this stack, this method will call [[ClassifyNewTrack()]] on all of those tracks. This method is therefore used to reclassify those particles into the correct stack. 

All of these tracks will be classified. If they are put into the **Urgent** stack, they will be the first tracks to be processed at the start of the new event.

This example continues from [[NewStage()]]. Since the user wants to track the number of _stage_ for each event, this value must be reset after each event. This method is perfect for that since it is called at the start of an event. This example is shown below:
```cpp
void ExampleStackingAction::PrepareNewEvent() {
	numberOfStages = 0;
}
```

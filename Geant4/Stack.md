A stack is an array of [[Track]] objects that are to be processes by the program during an [[Event]]. It is represented by the [`G4TrackStack`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/event/include/G4TrackStack.hh) class. The stack follows a _last-in-first-out_ scheme. When a track needs to be processed, it is popped off the stack

By default, geant4 has 3 stacks:
1. **Urgent**
2. **Waiting**
3. **PostponeToNextEvent**
However, the user can create more stacks if needed.

[[Track]] objects are added to the stacks via the [`G4EventManager`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/event/include/G4EventManager.hh). Stacks are then managed using the [`G4StackManager`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/event/include/G4StackManager.hh) class.

The data flow of popping and pushing tracks to stacks are as follows:
1. During an [[Event]] tracks can _only_ be popped from the **Urgent** stack.
2. Once the **Urgent** stack is empty, all the tracks in the **Waiting** stack are transferred over to the **Urgent** stack.
3. An [[Event]] ends when the **Urgent** and **Waiting** stacks are empty. 
4. Before the next event starts, all the tracks in the **PostponeToNextEvent** are pushed onto the **Urgent** stack for processing before new primary particles are generated. 


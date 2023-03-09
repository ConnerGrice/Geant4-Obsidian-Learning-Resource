## The Run Manager

The first step in the main function is to create a `RunManager`:

```CPP
auto* runManager = G4RunManagerFactory::CreateRunManager();
```

Once the `runManager` is declared, the next step will be to initialize the mandatory classes and give them to the `runManager`. These classes are as follows:

- [[DetectorConstruction]]
- [[PhysicsList]]
- [[PrimaryGeneratorAction]]

```cpp
runManager->SetUserInitialization(new ExampleDetectorConstruction);
runManager->SetUserInitialization(new ExamplePhysicsList);
runManager->SetUserInitialization(new ExamplePrimaryGeneratorAction);
runManager->Initialize();
```

There exist some optional action classes to further modify how a program would run. These are:

- [[RunAction]]
- [[EventAction]]
- [[StackingAction]]
- [[TrackingAction]]
- [[SteppingAction]]

These classes can be placed into an [[ActionInitialization]] class, meaning that this class can be passed into the `SetUserInitialization` function instead of them all individually.

## Visualisation Manager
If you want the program to use the visualiser, the next step would be to initialize that.
```cpp
G4VisManager* visManager = new G4VisExecutive;
visManager->Initialize();
```

In order to use the visualiser, you need to use the **user interface manager**. After getting this manager, the visualiser will be told what to do using a `.mac` file containing the instructions. 

To get the UI manager:
```cpp
G4UImanager* UImanager = G4UImanager::GetUIpointer();
UImanager->ApplyCommand(command)
```

Where `command` is some string that will call a macro file that will either define the visualiser options or define tell the program to run in **batch mode**.

```ad-def 
**Batch mode**:
This is when the program will run all at once within the terminal, removing the need to open the visualiser and run individual experiments. 
```

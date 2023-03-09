This class is used to consolidate all the custom user action classes. It is a child class of the [`G4VUserActionInitialization`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/run/include/G4VUserActionInitialization.hh) base class. The only abstract method that the user created class must define is the [[Build()]] method. 

The action classes that can be set within this class are:
1. [[PrimaryGeneratorAction]]
2. [[RunAction]]
3. [[EventAction]]
4. [[StackingAction]]
5. [[TrackingAction]]
6. [[SteppingAction]]

An example of a simple header file is given below:
```cpp
class ExampleActionInitialization: public G4VUserActionInitialization{
public:
	ExampleActionInitialization();
	~ExampleActionInitialization();
public:
	void Build() const;
};
```
This method is called whenever a hit is detected and data must be recorded. It is what defines what data is collected with each hit. This is done by getting at the instance of detection e.g. `G4Step`. Once the data is collected, it can be placed inside a [[Hit]] object. This is essentially a container for data. This example code continues from the [[Hit]] example:
```cpp
G4bool ExampleSD::ProcessHits(G4Step* astep,G4TouchableHistory*)){
	//Get the position of the particle
	auto position = aStep->GetPreStepPoint()->GetPosition();

	#Create a hit object and fill it with data
	auto hitPosition = new ExampleHit;
	hitPosition->SetPosition(position);
	
	//Put hit into the collection
	fexampleHitsCollection->insert(hitPosition);
	
	return true;
}
```
In this example `position` is found using the `aStep` object. This is the instance of the simulation of the particle that hit the sensitive detector. The `GetPreStepPoint()` method gets the particle at the beginning of the step, where `GetPostStepPoint()` would get the particle at the end of the step. `GetPosition()` will then get the position of the particle at that point.

Once this data is collected, a [[Hit]] container is created as `hitPosition`. The data is then inserted into the container, and the container is added to the hit collection using `->insert(hitPosition)`.
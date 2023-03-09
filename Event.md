An event is the second highest layer time scale in Geant4, with [[Track]]s being one level smaller and [[Run]]s being one level higher. An event is accessed via the [`G4Event`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/event/include/G4Event.hh) class. 

The _start of an event_ occurs when the primary particles are generated. Once this happens, the [[Track]]s associated to these particles are pushed onto a [[Stack]], Each particle is then popped off the [[Stack]] and goes goes through the [[TrackingAction]]. Any secondary particles produced during the tracking are then pushed back onto the [[Stack]]. This repeats until the [[Stack]] is empty, indicating that the _event is over_.

The event object will be initialised with a list of:
- Primary vertices
- Primary particles

During the event, other objects will be collected for use at the end of the event:
- [[Hit]] and hits collections
- [[Trajectory]]
- [[Digi]] (Digitized hits) and digi collection

Once the event is complete, the user will have access to these complete collections.
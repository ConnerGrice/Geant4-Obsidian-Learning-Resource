A track is similar to a [[Step]] however, the track is a single _snapshot_ of a particle as it exists in the simulation instead of the difference of particle properties between steps given by [[Step]]. The class the represents a track is the [`G4Track`](https://gitlab.cern.ch/geant4/geant4/-/blob/master/source/track/include/G4Track.hh).

The track holds some useful constant information as well as some information that is useful at each instance:

- Particle mass
- Particle Charge
- Particle Type

Since the track is the most recent state of the particle it will hold some data that is also help within the [[Step]] `PostStepPoint()` method, because that give the information about the particle at the very end of the timestep (most recent info).

If the user wants to use the state of the particle as it moves within the simulation, they must just the [[Trajectory]] object, which is a list of tracks.

There are some conditions that, if met, will cause the track to be deleted:
- Particle reaching the end of the `world` volume
- Particle decays
- Loses all of its kinetic energy
- Force stopped by user
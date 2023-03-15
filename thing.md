* contention systems: collision and rename to fix
    * low load environement
* contention free: no collisions
    * high load environment where we don't want any collisions

Contention on a bus environment
* IEEE 802.1
    * .2
    * .3 - contention environment; CSMA/CD; LAN standard
    * .4 - token passing mechanism
    * .5 - token passing mechanism
### .3
* Jam Signal: 3 bytes of ones meant to reenforce the collision
* binary exponential backoff algorithm
* contention interval, where the contention can happen
    * length of the wire is the contention interval
### .4, .5
* token passing mechanism
* high load environment is when only one station is allowed to talk at a time
* bounded weight (this is not in a contention environment)
* first watchdog station wants to see a free token
    * sets off the alarm saying there isn't a new one coming and spits out a new free token in place of the station that "blew up"
    * we have watchdog 2, 3, etc. as a backup
* only one thing worse than no token is two of them
* token ring advantage- time and distance don't matter
* token passing mechanism for a token bus is a simulator
* contention ring- starts in an eithernet style environment, when you run into issues spit out another free token, then shift back when it calms down
    * it gives you both the best and the worst of both worlds becuase it constantly is switching under normal circumstances.
# lv-interface-re

For context, this is a proof of concept, it doesn't do anything special and I haven't (yet) coded anything to communicate between the different re-entrant VIs. The interior code is identical to the NRE example and upon closing the launch window the VI references for any launched interfaces will be killed (since the parent VI is no longer running).

## Getting Started

Run the launcher.vi and click the launch button.

## Guidelines/Opinions

In my opinion, there are very few use cases that can take advantage of a re-entrant interface, most interfaces i've developed have been non re-entrant due to their use cases. 

In a perfect world, there would be an event that would allow 1:N communication that could gracefully close any re-entrant VIs before stopping the launcher.vi
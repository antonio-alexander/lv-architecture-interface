# lv-interface-nre

For context, this architecture was developed with the idea that very simple or no functionality would be ACTUALLY implemented within it. It assumes that only the API for your functionality or "launchers" to the new functionality, would be present within it (to maintain its simplicity).

The expected use case for this is for it to be non re-entrant, meaning that there is only ONE instace of this interface in a runtime/application instance.

This interface is split into four loops/threads:

 * main - this loop is kinda useless, but serves as a kind of origin, anything that you "want" to happen that's intrinsic or requires a quick response time (e.g. attempting to close the window), should occur here rather than somewhere else. As coded, it's the last while loop to "stop".
 * control - this loop is meant to involve all controls/inputs, if the user clicks a button, it's event case would be in this loop (rather than somewhere else).
 * interface - this loop is meant to regularly update information with the UI, e.g. if you're periodically updating a set of indicators. This should only involve READ-ONLY data. Keep in mind that although it uses an event structure for timing,under some use cases it might not update at the configured rate (e.g. events are configured). IF you have events that give you information to update indicators, they should be registered for this event structure.
 * feedback - this loop is meant to provide feedback for when something happens. It's separated specifically because some feedback can block which would otherwise "pause" the remainder of the interface. An example would be displaying an error, if an error were to happen, you could use the simple error handler to display the message, but you don't want to stop everything else from happening while you're waiting on the user to click OK (under certain circumstances).

## Getting Started

Do the following steps to get started with this template/pattern:

 1. Right click the lv-interface-nre.lvlib library and save-as; store it in a separate folder.
 2. Open main.vi
 3. Copy+paste and/or populate the front panel with controls and indicators.
 4. Add event cases for all the controls on the front panel that don't handle essential functions (i.e. anything that would affect the process of the interface)to the event structure for the control loop.
 5. Edit the event structure for the interface loop to handle population of data for all indicators. Add anything that's polling based to the timeout case.
 6. IF you have drop-downs, edit/replace the manu.rtm, edit the menu_selection.ctl in ./private/_controls/menu_selection.ctl to mirror the selections and edit the Menu Selection case in the control loop appropriately.
 7. Profit. 

## Guidelines/Opinions

Below are some guidelines that can help provide guard rails when implementing this pattern:

 * I think it's really easy to go overboard with the events, try not to add them unless you really need them. Other than the die command, the loops are expected to be fairly independent, if you need them to interact, you should use local_interface or local_common to transport those actions.
 * HMI operations or any operations that involve control references should be done using the references cluster. I advise against having ANY property/invoke nodes linked to controls in main. Not only is it ugly, it's not very portable once you start moving things around.
 * Events don't have a lot of feedback, any time you use events, you should not plan on getting feedback for success (use the feedback loop for that maybe). I think if you find you really need this, you're using the wrong tool and you should modify the architecture to support that kind of blocking feedback (e.g. use a single element queue for feedback).
 * I think it makes a lot of sense to separate your code into interfaces and functional modules (like model view view model), as a result you may require a kind of launcher to bootstrap everything.

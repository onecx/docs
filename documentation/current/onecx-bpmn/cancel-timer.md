# BPMN: Cancel Timer

Sometimes the business case requires that the set timer needs to be manually canceled so that the process can continue further. For this purpose, it is ideal to use an exclusive event-based gateway that enables work with events.

The process instance enters the gateway and waits there until one of the events behind the gateway is triggered. The decision about the path which will be taken is done by someone out of the process or by time event. Only one path can be triggered.

So there might be a positive path, when event `action received` occurs (i.e. received callback as expected). In this case the sequence flow 1 is taken and an activity to process item follows. Sometimes it can take longer to get the wished action to be done. A `timer event` can be used 3 to wait till the action is done or to set as a maximum time space for carrying out the action. Waiting for the action can be also interrupted earlier (cancelled) by other way of solving the situation (i.e. manually) outside the green path 2, so that the item can be processed further anyway.

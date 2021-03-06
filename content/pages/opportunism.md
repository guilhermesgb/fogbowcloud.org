Title: Opportunism
url: opportunism
save_as: opportunism.html
section: arch
index: 3

Opportunism
==========
Opportunism is a feature that allows idle resources to be used by the cloud. Resources being used by a local user shouldn’t show up to the cloud.

## Requirements
* nova-compute should be disabled and its instances killed when there is mouse/keyboard activity.
* it must come back when the host is idle for a certain amount of time.

## Implementation
### Monitoring
The monitoring is implemented using PowerNap that is a configurable deamon that executes some actions when the system is idle, and the idleness is determined by monitors that can be configured to watch CPU load, processes, mouse/keyboard, etc.

In default version, powernap allows to customize an action script to determine the action to be executed when the system is idle, but doesn't have a way to define the action executed when the system is back in activity.

The powernap version used in this project was customized to allow the use of a custom recover action script.

### Action
A powernap action script needs to be written sends an RPC to nova-compute in order to disable it.

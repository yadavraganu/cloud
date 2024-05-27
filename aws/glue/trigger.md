When fired, a trigger can start specified jobs and crawlers. A trigger fires on demand, based on a schedule, or based on a combination of events.
There are three types of triggers:

## Scheduled
A time-based trigger based on cron.
## Conditional
A trigger that fires when a previous job or crawler or multiple jobs or crawlers satisfy a list of conditions.
When you create a conditional trigger, you specify a list of jobs and a list of crawlers to watch. For each watched job or crawler, you specify a status to watch for, such as succeeded, failed, timed out, and so on. The trigger fires if the watched jobs or crawlers end with the specified statuses. You can configure the trigger to fire when any or all of the watched events occur.

## On-demand
A trigger that fires when you activate it. On-demand triggers never enter the ACTIVATED or DEACTIVATED state. They always remain in the CREATED state.
So that they are ready to fire as soon as they exist, you can set a flag to activate scheduled and conditional triggers when you create them.

<hr/>

##### Speaker: Althaf Hameez (Senior Engineering Manager from Grab)

##### Topic: SRE / DevOps sharing by Grab

##### Date: 3/3/2023

<hr/>

` For Grab, customers depend heavily on us -- a good problem`
` "Hope is not a strategy", "I hope that this won't go wrong"`

<h6>When it comes to DevOps, one big issue is development speed vs stability</h6>

- Introduce processes
- Change is always the cause of issues
- Grab has a `rollback first policy`, anything went wrong, rollback to the previous version that is in good state.
- Grab evaluates processes based on the number of rollbacks vs deployments lol

- Grab has this ceremony for company-wide engineer sharing each month to share about post-mortems

  - Team A makes the same mistakes made by team B 3 months ago...? Experience and knowledge is shared across engineers.
  - Give incentives to presenter
  - Give incentives to attendees?

##### Feature flag

- Rolling out different features in different cities
- Dynamic config (redis.?)
- Build UI for toggle
- This means Grab can change things on the fly

#### Incident examples

###### Vietnam incident

- All users have their default map pointing to Africa (coordinate at 0,0), somehow.
- Debugging from the backend, realize BE couldn't parse the coordinate correctly.
- Actual reason: Grab did localization at vietnam, (, -> . for decimal), screwed up the parser for coordinate system

###### 2015 Singapore Grab break down

- In Singapore, there was 1 day in 2015, blue line MRT + purple line MRT breakdown, grab breakdown as a result and you know why🫠

#### Critical Path Analysis:

- It's better to have a sub-par customer experience when booking a ride, than having no experience to book a ride.
- Shut down some microservices at 1am / 2am to observe the change / complaint?
- This is to identify which services are the utmost critical for the happy path on booking a ride

##### Project Swarm

- Distribute SRE powers to Swarm SREs in teams
- Every engineer becomes a Swarmer
- You build it, you run it

### Monitoring

#### 1. Under-alerting is better than over-alerting

- Start a good culture on what it means to be on-call, alert fatigue and proper review of metrics and alarms
- CPU utilization hits 80%, hits an alert, but is it necessary? Not at all, if we have a auto-scaling group. (not actionable)
- Paging should really mean something wrong

#### 2. Define & Alert on Major Business Metrics

- CPU utilization, memory, latency only tells half the story.
- Track rides compared to previous week at 15-min interval (major business metrics)
- Can predict weather based on the rides metrics 😅

#### 3. Have alarms that fire provide first steps to responders

#### 4. Standardize your monitoring & alerting stack

- sentry, datadog, ....
- The more standardardized your metrics and alerting stack, the more people can help investigate and troubleshoot during and after an incident.
- Because monitoring tools do have some learning curves
- Grab has a `grabkit` with golang to standardize coding and monitoring stacks.

#### Preparing for incident

##### Pre-ready outage call

- Setup channel on Slack, undismissable.
- Dedicated video conferencing call link readt to go for outage so that if something is wrong people already know where to join.

##### Incident commanders

- Clear understanding of who leads an incident call
- Otherwise the calls will be indecisive and chaotic
- Can override CEO, have full say
- See PagerDuty guideline
- Can we turn off this feature, is there a problem? Yes or No? Can't afford to listen to long-winded answer.

##### Involvement from non-tech

##### More practice

- practice, simulate, fire drills, try bring down some services

#### During an incident

##### Knowing what changed

- Change is a frequent cause of issues.
- In Facebook there are 2 weeks that never have incident. Peer review week and Christmas week
- Knowing what is changed is important in reverting changes.
- say, payment service faces latency issue, it could be because payment service is calling the geo service to get the routing to calculate the fare, payment service team should coordinate with geo service team to check what goes wrong.

##### Getting to last known good state

- Have rollback back binary ready.
- Make the rollback process faster than deployment

##### forming a hypothesis on cause

#### Postmortem & Processes

##### Blameless culture

- Doesn't mean there is not accountability
- Engineer's mistake is the least priotity
- Systems should be made such that it will be hard for people to make mistake!
- Managers will be the ones leading the postmortem call (to hold accountability), because generally managers have better communication skills, they know what actionable items to prioritize .
- No performance penalty

##### Postmortems

`Never let a good crisis go to waste --- Winston Churchill`

- Consolidate all postmortems read in one place (say, Confluence), make it visible to everybody.
- Define good Action Items (AIs), short-term & long-term
- Near misses are as important as incidents

### Platform Engineering

- Provide a paved path (for engineers), create scaffold for golang (like grabkit)
- Engineers create a service -> auto-generate dashboard for analytics
- Help accelerate service teams
- Simplified and automated

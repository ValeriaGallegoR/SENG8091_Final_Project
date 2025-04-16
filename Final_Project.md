# EPIC 1: IMPROVED BUS SCHEDULE

**As** a passenger who wants to travel to New Hamburg,

**I want** the 77 bus to operate earlier in the morning and later in the evening,

**To** have the flexibility to travel at any time of day that suits my needs.

### Assumption:

Passengers would use the bus service more frequently if the operating hours were extended. And the highest passenger flow can be early in the morning and late in the evening.

### Validations (Questions):

- What specific early morning and late evening time slots do passengers prefer?
- How many passengers currently avoid the bus due to its limited hours?
- Would extended hours attract new users or just better serve existing ones?
- How much additional cost would extend service hours introduce, and is it justifiable by projected usage?
- GRT has previously tried to extend schedules? what was the result?

## REQUIREMENTS 

## Functional Requirements

### EPIC_1_REQ_1:

**As** a passenger
**I want** the 77 bus to run services before 7 AM
**To** be able to travel to New Hamburg early in the morning.

**Purpose:** Support passengers with early work shifts or travel needs.

### Tasks

#### Task_01: Extend bus route scheduling system to include services before 7 AM.

**_Solution_**

```bash
addService(routeId: int, departureTime: datetime) → bool
```
```bash
generateEarlyTrips(routeId: int, startTime: datetime, endTime: datetime) → List[Trip]
```
```bash
 updateTimetable(routeId: int, trips: List[Trip]) → bool
```

**_Outcome_**

The 77 bus route now includes early morning departures starting at 5:30 AM, supporting early travelers to New Hamburg

### EPIC_1_REQ_2:

**As** a passenger
**I want** the 77 bus to run services after 7 PM
**To** return from New Hamburg later in the evening.

**Purpose:** Provide flexibility for evening events, late work shifts, or emergencies.

### Tasks

#### Task_01: Update scheduling logic to add services after 7 PM.

**_Solution_**

```bash
addService(routeId: int, departureTime: datetime) → bool
```
```bash
generateEveningTrips(routeId: int, startTime: datetime, endTime: datetime) → List [Trip]
```
```bash
updateTimetable(routeId: int, trips: List [Trip]) → bool
```

_**Outcome**_

The 77 bus route operates until 10:00 PM, giving passengers flexibility for evening travel from New Hamburg.

###  EPIC_1_REQ_3:
**As** a passenger
**I want** the updated bus schedule to be published online and at stations
**To** easily plan my trip.

**Purpose:** Ensure passengers are informed about the new operating hours.

### Tasks

#### Task_01: Automate the publication of the updated schedule to the public website.

**_Solution_**

```bash
publishToWeb(timetable: Timetable) → bool
```
```bash
updateSchedulePage(timetable: Timetable) → bool
```
```bash
validateWebPublication(routeId: int) → bool
```

**_Outcome_**
Passengers can view the latest bus schedule on the website immediately after updates, ensuring online trip planning is always accurate.

#### Task_02: Update and synchronize physical station displays with the new schedule.

_**Solution**_

```bash
refreshStationDisplays(timetable: Timetable) → bool
```
```bash
syncWithCentralSystem(stationId: int) → bool
```
```bash
publishToStations(timetable: Timetable) → bool
```

_**Outcome**_

All physical station displays reflect the updated schedule, providing clear and consistent information for passengers at stations.

## Non-functional Requirements

### EPIC_1_REQ_4:
**As** a system administrator
**I want** all schedule changes to propagate across all digital platforms (mobile app, web app, station screens) within 10 seconds of update
**To** ensure consistent and accurate passenger information.

**Purpose:** Real-time data synchronization to prevent outdated schedules.

### Tasks

#### Task_01: Implement event-driven architecture for real-time propagation.

**_Solution_**

```bash
publishScheduleUpdateEvent(timetable: Timetable) → bool
```
```bash
onScheduleUpdate(event: ScheduleUpdateEvent) → bool
```
```bash
dispatchToAllChannels(event: ScheduleUpdateEvent) → bool
```

**_Outcome_**

Schedule updates are instantly pushed to all platforms (mobile, web, station screens), ensuring updates reach passengers within 10 seconds

### EPIC_1_REQ_5:
**As** a system administrator
**I want** the scheduling backend to support zero downtime deployments
**To** allow updates to bus operating hours without service interruption.

**Purpose:** High availability during schedule changes.

### Tasks

#### Task_01: Implement deploy to a parallel environment and switch traffic only after validation.

_**Solution**_

```bash
deployNewVersion(versionId: string) → bool
```
```bash
switchTrafficToNewVersion() → bool
```
```bash
validateNewDeployment(versionId: string) → bool
```

**_Outcome_**

New deployments happen on a separate environment and traffic is only switched when it's healthy, ensuring zero service interruption.

### EPIC_1_REQ_6:

**As** a system administrator
**I want** an automated audit trail of schedule modifications stored in a secure log 
**To** ensure traceability and compliance.

**Purpose:** Enable accountability and system monitoring.

### Tasks

#### Task_01: Log all schedule modification events securely.

_**Solution**_

```bash
logScheduleChange(userId: int, changeDetails: string, timestamp: datetime) → bool
```
```bash
storeLogEntry(logEntry: LogEntry) → bool
```

_**Outcome**_

Every schedule change is automatically logged and securely stored, ensuring full traceability and compliance with audit requirements.


# EPIC 2: ADDITIONAL ROUTES AND STOPS

**As** a passenger who wants to travel to New Hamburg,

**I want** more convenient bus stops and routes,

**To** reach New Hamburg more directly without long detours or transfers.

### Assumption:

More direct or expanded routes to New Hamburg will reduce travel time and increase passenger satisfaction.

### Validations (Questions):

- Which neighborhoods or areas are underserved by the current route to New Hamburg?
- How much time would passengers save with a more direct or expanded route?
- Would more stops increase accessibility without making the trip too long?
- Are there alternative routes or connections that passengers prefer but are currently unavailable?
- What is the estimated increase in ridership if the route coverage improves?
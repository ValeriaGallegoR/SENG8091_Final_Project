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

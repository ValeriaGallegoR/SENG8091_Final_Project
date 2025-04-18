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

## REQUIREMENTS 

## Functional Requirements

### EPIC_2_REQ_1:

**As** a passenger

**I want** new stops added closer to residential areas

**To** reduce walking distance to the bus.

**Purpose:** Increase convenience and accessibility.

### Tasks

#### Task_01: Analyze residential density to identify underserved areas.

**_Solution_**

```bash
getHighDensityAreas() → List[GeoLocation]
```

```bash
findAreasWithoutStops(densityAreas: List[GeoLocation], existingStops: List[BusStop]) → List[GeoLocation]
```

**_Outcome_**

Identifies specific residential zones lacking nearby bus stops.

#### Task_02: Plan and integrate new stops into the route.

**_Solution_**

```bash
proposeNewStops(locations: List[GeoLocation]) → List[BusStop]
```

```bash
addNewStopToRoute(routeId: int, stop: BusStop) → bool
```

_**Outcome**_

New stops are added in residential areas, reducing passenger walking distances.

### EPIC_2_REQ_2:

**As** a passenger

**I want** the 77 route to connect with other major transit lines

**To** reduce the need for multiple transfers.

Purpose: Improve journey efficiency and attract more riders.

### Tasks

 #### Task_01: Identify major transit hubs and analyze route gaps.

**_Solution_**

```bash
getMajorTransitHubs() → List[GeoLocation]
```

```bash
findMissingConnections(routePath: List[GeoLocation], hubs: List[GeoLocation]) → List[GeoLocation]
```

**_Outcome_**

Pinpoint’s locations where the 77 route lacks connections to major transit lines.

#### Task_02: Update route and synchronize schedules with connecting lines.

_**Solution**_

```bash
adjustRouteForConnections(routeId: int, hubs: List[GeoLocation]) → bool
```

```bash
syncSchedulesWithTransitLines(routeId: int, transitLineId: int) → bool
```	

**_Outcome_**

The 77 route is extended to link with major lines, and schedules are coordinated for smoother transfers.

## Non-functional Requirements

### EPIC_2_REQ_3:

**As** a system administrator

**I want** the system to support flexible route configurations

**To** easily accommodate future expansions or changes to the New Hamburg service area.

**Purpose:** Ensure the software can handle complex and growing route networks without major redesign.

### Tasks

#### Task_01: Design a modular route configuration system to support dynamic changes.

**_Solution_**

```bash
createNewRouteConfiguration(routeId: int, configurationData: RouteConfigData) → bool
```
```bash
modifyRouteConfiguration(routeId: int, configurationData: RouteConfigData) → bool
```
```bash
checkRouteDependencies(routeId: int) → List[Route]
```
```bash
validateRouteConfig(routeId: int, configurationData: RouteConfigData) → bool
```

**_Outcome_**

The system allows dynamic creation, modification, and validation of route configurations, enabling easy expansion and adjustments to the New Hamburg service area without major redesigns.

### EPIC_2_REQ_4:

**As** a system administrator

**I want** the application to efficiently manage and display multiple overlapping routes

**To** help passengers clearly understand their options to reach New Hamburg.

**Purpose:** Improve user experience when multiple route choices are available for the same destination.

### Tasks

#### Task_01: Implement an intelligent route visualization system for overlapping routes.

**_Solution_**

```bash
generateOverlappingRouteVisual(routeIds: List[int]) → Image
```
```bash
optimizeRouteDisplay(routeIds: List[int]) → List[RouteSegment]
```
```bash
updateRouteDisplay(routeVisualization: Image) → bool
```

**_Outcome_**

The system efficiently displays overlapping routes in an intuitive visual format, helping passengers easily understand their options to reach New Hamburg.

# EPIC 3: REAL-TIME TRACKING AND NOTIFICATIONS

**As** a passenger who wants to travel to New Hamburg,

**I want** real-time updates on bus location and arrival times,

**To** plan my journey more efficiently and avoid long waits at stops.

### Assumption:

Real-time updates will reduce uncertainty and improve the travel experience for passengers heading to New Hamburg.

### Validations (Questions):

- What notification methods (mobile app, SMS, station displays) do passengers prefer?
- How accurate and timely can the real-time data be for the 77 bus?
- Are there technical challenges in integrating the 77 bus route into a real-time tracking system?

## REQUIREMENTS 

## Functional Requirements

### EPIC_3_REQ_1:

**As** a passenger

**I want** to see real-time arrival estimates for the 77 bus

**To** minimize waiting time at stops.

**Purpose:** Improve passenger satisfaction with timely information.

### Tasks

#### Task_01: Implement real-time tracking and estimation of bus arrival times.

_**Solution**_

```bash
trackBusArrival(routeId: int, stopId: int) → BusArrivalEstimate
```
```bash
calculateArrivalEstimate(busLocation: GeoLocation, stopLocation: GeoLocation) → datetime
```
```bash
updateArrivalEstimate(estimate: BusArrivalEstimate) → bool
```

**_Outcome_**

The system provides real-time estimates for bus arrivals, helping passengers minimize waiting times at stops.

### EPIC_3_REQ_2:

**As** a passenger

**I want** to receive notifications about delays on the 77 bus route

**To** adjust my travel plans accordingly.

**Purpose:** Provide proactive communication.

### Tasks

#### Task_01: Implement a notification system for bus delays.

**_Solution_**

```bash
monitorDelays(routeId: int, delayThreshold: int) → List[DelayEvent]
```
```bash
sendDelayNotification(userId: int, delayEvent: DelayEvent) → bool
```
```bash
getUserNotificationPreferences(userId: int) → NotificationPreferences
```

**_Outcome_**

Passengers receive timely notifications about delays, allowing them to adjust their travel plans accordingly.

## Non-functional requirements

### EPIC_3_REQ_3:

**As** a system administrator

**I want** the system to support dynamic service hours configurations

**To** easily extend or modify bus operation times without needing code changes.

**Purpose:** Enable flexible scheduling to adjust operating hours for special events or permanent changes.

### Tasks

#### Task_01: Develop a service hours configuration manager to allow dynamic adjustments of bus operating times.

**_Solution_**

```bash
setServiceHours(routeId: int, startTime: datetime, endTime: datetime) → bool
```
```bash
getServiceHours(routeId: int) → ServiceHours
```
```bash
validateServiceHours(startTime: datetime, endTime: datetime) → bool
```

**_Outcome_**

The system allows administrators to dynamically set and update bus operating hours without code changes, enabling quick adjustments for special events or permanent changes.

### Task_02: Implement a user interface for administrators to manage and update service hours.

**_Solution_**

```bash
showServiceHoursForm(routeId: int) → ServiceHoursForm
```
```bash
updateServiceHoursForm(routeId: int, newHours: ServiceHours) → bool
```
```bash
notifyUpdateToAdmin(routeId: int, updateStatus: bool) → bool
```

_**Outcome**_

Admins can easily adjust and save changes to bus service hours using a simple interface, ensuring that updates are visible and communicated across the system.

### EPIC_3_REQ_4:

**As** a system administrator

**I want** the system to handle time-based rules for service availability

**To** ensure that journey planners and schedules accurately reflect extended service periods.

**Purpose:** Avoid confusion by only showing valid options for the passenger’s time of travel.

### Tasks

#### Task_01: Create a time-based rule engine that filters available routes based on the current time.

**_Solution_**

```bash
getAvailableRoutes(currentTime: datetime) → List[Route]
```
```bash
setServiceTimeRules(routeId: int, startTime: datetime, endTime: datetime) → bool
```

**_Outcome_**

The system filters and displays only the valid routes for the current time, ensuring that passengers only see available options during their journey period.

#### Task_02: Implement dynamic rule management for special service hours

**_Solution_**

```bash
createSpecialServiceRule(routeId: int, specialDate: datetime, startTime: datetime, endTime: datetime) → bool
```
```bash
validateSpecialServiceRule(routeId: int, currentDate: datetime) → bool
```
```bash
adjustPlanForSpecialService(currentDate: datetime, routeId: int) → List[Route]
```	

_**Outcome**_

Time-based rules are applied dynamically to manage extended service hours or changes for special events, ensuring accurate scheduling for passengers during unique periods.
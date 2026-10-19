# Field service day plan

_Generated 2026-10-19 04:50Z. Drive times are real road-network minutes from OSRM; addresses geocoded with OpenStreetMap Nominatim._

## Ana - shift 08:00-17:00, 2 jobs, 8.2 min driving, finishes 10:50

| # | Customer | Arrive | Drive to it |
| - | - | - | - |
| 1 | Harbor Dental | 09:00 | 3.0 min |
| 2 | Nob Hill Salon | 10:05 | 5.1 min |

**Free windows (backfill candidates):**

- 08:00-08:57 free, 57 min
- 370 min free at the end of the day

## Ben - shift 09:00-18:00, 4 jobs, 28.8 min driving, finishes 15:19

| # | Customer | Arrive | Drive to it |
| - | - | - | - |
| 1 | Potrero Gym | 09:05 | 4.7 min |
| 2 | Bayview Clinic | 11:00 | 5.2 min |
| 3 | Mission Cafe | 12:37 | 6.9 min |
| 4 | Sunset Auto | 14:04 | 12.0 min |

**Free windows (backfill candidates):**

- 10:05-10:55 free, 50 min
- 13:22-13:52 free, 30 min
- 161 min free at the end of the day

## Backfill - what the free minutes can absorb

- **Ana 08:00-08:57** (57 min free): no unscheduled job left to fill it; the remaining jobs sit on Ben and would only move if the travel saved beats the drive
- **Ben 10:05-10:55** (50 min free): no unscheduled job left to fill it; the remaining jobs sit on Ana and would only move if the travel saved beats the drive
- **Ben 13:22-13:52** (30 min free): no unscheduled job left to fill it; the remaining jobs sit on Ana and would only move if the travel saved beats the drive

### Reading this plan

- **Drive minutes are road-network minutes** from an OSRM routing engine on OpenStreetMap data, not straight-line distance divided by a guess.
- Each technician's sequence is built by cheapest-insertion and then improved with 2-opt, so the plan does not cross itself the way a first-pass greedy route does.
- Free windows are the minutes between the end of one job (plus the drive to the next) and the next arrival; end-of-day capacity is what is left before the shift ends.
- A free window is only useful if work exists within reach of it - that is what the backfill lines state.

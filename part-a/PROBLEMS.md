# IRCTC Problem Discovery — Part A


## Summary

- Total problems documented: 6
- Platform explored: irctc.co.in
- Devices used: Desktop Chrome and Mobile Browser


---

# Problem 1: Tatkal Booking Crashes at 10:00 AM [Given]


## What is broken:

During Tatkal booking opening time, IRCTC becomes extremely slow or unavailable. Users experience page loading failures, session errors, and no useful feedback about their position or booking status.


## Affected users:

Tatkal passengers, emergency travelers, students, employees, and users trying to book limited quota tickets.


## Frequency:

Occurs daily during Tatkal opening time:
AC classes: 10:00 AM
Non-AC classes: 11:00 AM


## Current flow:

1. User opens IRCTC website around 9:50 AM.
2. User logs in and searches train details.
3. User selects Tatkal quota.
4. User waits until booking opens.
5. At 10:00 AM user clicks Book Now.
6. Website becomes slow or shows errors.
7. User refreshes multiple times.
8. User finally enters booking page.
9. Tatkal seats are already unavailable.


## Where exactly it breaks:

Step 5.

The system receives very high traffic at the same time and does not provide queue management, progress status, or failure explanation.


---

# Problem 2: Search Filters Do Not Work Reliably [Given]


## What is broken:

Train search filters sometimes fail to update results correctly.


## Affected users:

Passengers searching specific trains based on timing, class, and availability.


## Frequency:

Frequently during train searches, especially with many search conditions.


## Current flow:

1. User opens IRCTC.
2. User enters source station.
3. User enters destination station.
4. User selects journey date.
5. User applies class filter.
6. User applies availability filter.
7. User checks results.
8. User changes filters again.
9. Results sometimes remain unchanged.


## Where exactly it breaks:

Step 7.

The filter state is not always synchronized with search results.


---

# Problem 3: Seat Selection Resets [Given]


## What is broken:

Selected berth preference may disappear after moving to passenger details.


## Affected users:

Passengers who require specific seats like lower berth, senior citizens, and families.


## Frequency:

Observed during booking flow, especially on mobile browsers.


## Current flow:

1. User searches train.
2. User selects train.
3. User enters passenger details.
4. User opens seat preference.
5. User selects lower berth.
6. User proceeds.
7. Passenger page opens.
8. Selected berth preference is missing.


## Where exactly it breaks:

Step 8.

Seat preference data is not properly carried between booking screens.


---

# Problem 4: PNR Status Information Is Hard To Understand [Self Discovered]


## How I found it:

While checking PNR status page.


## What is broken:

The status information contains technical railway terms that normal users may not understand.


## Affected users:

First-time travelers and passengers checking waiting list confirmation.


## Frequency:

Every day when users check booking status.


## Current flow:

1. User opens IRCTC.
2. User selects PNR status.
3. User enters PNR number.
4. User receives ticket status.
5. User sees codes like RAC/WL/CNF.
6. User searches meaning separately.
7. User remains unsure about travel possibility.


## Screenshot:

Added in assets/screenshots/


## Where exactly it breaks:

Step 5.

The platform displays status without enough explanation or guidance.


---

# Problem 5: Cancellation Flow Is Confusing [Self Discovered]


## How I found it:

Explored ticket cancellation process.


## What is broken:

Cancellation options and refund details are not clearly explained before confirmation.


## Affected users:

Passengers cancelling tickets and expecting refunds.


## Frequency:

Common because many passengers modify travel plans daily.


## Current flow:

1. User opens booked ticket.
2. User selects cancellation.
3. User views refund information.
4. User searches charges.
5. User confirms cancellation.
6. Ticket gets cancelled.
7. Refund processing begins.


## Where exactly it breaks:

Step 3.

Refund breakup is not presented clearly.


---

# Problem 6: Mobile Browser Experience Issues [Self Discovered]


## How I found it:

Opened IRCTC website on mobile browser.


## What is broken:

Mobile browser experience has small controls and difficult navigation.


## Affected users:

Users without access to IRCTC mobile app.


## Frequency:

Daily for mobile web users.


## Current flow:

1. User opens IRCTC mobile website.
2. User tries login.
3. User searches train.
4. User scrolls results.
5. User opens booking.
6. User fills details.
7. User navigates between pages.


## Where exactly it breaks:

Step 4.

The interface is not optimized for smaller screens causing navigation difficulty.

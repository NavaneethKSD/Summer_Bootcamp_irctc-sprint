# IRCTC Feature Specifications – Part B

This document contains feature specifications for the six problems identified in Part A. Each feature references the corresponding problem and proposes a practical solution with technical implementation details.

---

# Feature Spec 1: Tatkal Virtual Queue System

## Problem Statement

Part A identified that the IRCTC website becomes extremely slow during Tatkal booking at 10:00 AM and 11:00 AM due to a sudden surge in users. Most users repeatedly refresh the page, receive server errors, or lose their booking opportunity without knowing what happened.

## Current State (from Part A)

The booking process fails immediately after users click the "Book Now" button. Thousands of requests hit the server simultaneously, causing page timeouts and session failures.

## Proposed Solution

Instead of allowing everyone to enter the booking page at once, users are automatically placed into a virtual queue. They can see their queue position, estimated waiting time, and booking countdown.

## Proposed User Flow

1. User logs into IRCTC before Tatkal opens.
2. User selects train and passenger details.
3. User clicks "Join Tatkal Queue."
4. System assigns queue number.
5. User sees live queue position and estimated wait.
6. When their turn arrives, a notification appears.
7. User receives 90 seconds to complete booking.
8. Booking proceeds normally.

## Technical Implementation Plan

### System Components

- Frontend Booking UI
- Queue Management Service
- Backend API
- Database
- Notification Service

### New Data Requirements

New Queue Table

- Queue ID
- User ID
- Train Number
- Booking Time
- Queue Position
- Status
- Expiry Time

### API Changes

POST /tatkal/joinQueue

Creates queue entry.

GET /tatkal/queueStatus

Returns

- Position
- Estimated wait
- Remaining countdown

DELETE /tatkal/leaveQueue

Removes user from queue.

### Frontend Changes

- Queue Screen
- Live Progress Bar
- Countdown Timer
- Notification Popup

### Third Party Services

Firebase Cloud Messaging for browser notifications.

## Success Metrics

- Server crash reduced by 80%
- Booking completion increases from 40% to 70%
- Average waiting time visible to all users

## Edge Cases

- User closes browser
- Queue expires
- Internet disconnects
- Payment timeout
- Server restart

---

### Wireframe

![Tatkal Queue](../assets/wireframes/tatkal-queue.png)

*Figure 1: Proposed Tatkal Virtual Queue Interface*

# Feature Spec 2: Persistent Smart Search Filters

## Problem Statement

Users frequently apply filters like Sleeper Class, Available Seats, or Morning Departure. After refreshing or returning to search results, filters reset unexpectedly.

## Current State

Search filters do not always update results correctly and are lost after navigation.

## Proposed Solution

Filters remain saved during the search session until the user clears them manually.

## Proposed User Flow

1. User searches trains.
2. User selects filters.
3. Results update instantly.
4. User opens train details.
5. User returns.
6. Filters remain selected.
7. User modifies filters if required.

## Technical Implementation Plan

### System Components

- Search API
- Frontend
- Browser Session Storage

### New Data

Saved Filter Object

- Class
- Departure Time
- Availability
- Quota

### API Changes

GET /search?filters=

Returns filtered trains.

### Frontend

- Filter Chips
- Saved State
- Reset Button

### Third Party

None

## Success Metrics

- 95% filter persistence
- 30% reduction in repeated searches
- Faster booking completion

## Edge Cases

- Empty results
- Invalid filter combinations
- Session expiry

---

### Wireframe

![Search Filters](../assets/wireframes/search-filter.png)


# Feature Spec 3: Seat Preference Lock

## Problem Statement

Users select Lower Berth or Window Seat but their preference disappears during booking.

## Current State

Seat preference resets before payment.

## Proposed Solution

Seat preference remains locked throughout booking unless changed manually.

## Proposed User Flow

1. Search train.
2. Select passengers.
3. Choose seat preference.
4. Preference saved immediately.
5. Proceed to payment.
6. Review page shows selected berth.
7. Booking completed.

## Technical Implementation Plan

### Components

- Booking API
- Passenger Module
- Database

### New Data

Passenger Preference

- Passenger ID
- Berth Type
- Timestamp

### API

PUT /booking/preferences

Stores preference.

GET /booking/preferences

Fetches saved choice.

### Frontend

- Seat Selection Card
- Confirmation Label

### Third Party

None

## Success Metrics

- Seat preference retained in 99% bookings
- Reduced booking complaints

## Edge Cases

- Preferred berth unavailable
- Multiple passengers selecting same berth

---

### Wireframe

![Seat Preference](../assets/wireframes/seat-preference.png)



# Feature Spec 4: Simple PNR Status Dashboard

## Problem Statement

Many users cannot understand railway abbreviations like WL, RAC, and CNF.

## Current State

PNR page only displays codes.

## Proposed Solution

Provide plain-language explanations with travel guidance.

## Proposed User Flow

1. Enter PNR.
2. View status.
3. See explanation.
4. View confirmation probability.
5. Receive suggestions.

## Technical Implementation Plan

### Components

- PNR API
- Frontend
- Notification Service

### Data

Status Description Table

### API

GET /pnr/status

Returns

- Code
- Meaning
- Suggestion

### Frontend

- Status Card
- Progress Indicator
- Explanation Panel

## Success Metrics

- 60% reduction in support queries
- Higher user understanding

## Edge Cases

- Invalid PNR
- Server unavailable

---

### Wireframe

![PNR Dashboard](../assets/wireframes/pnr-dashboard.png)


# Feature Spec 5: Transparent Cancellation & Refund Tracker

## Problem Statement

Users are confused about refund amount and refund processing.

## Current State

Refund information is difficult to understand.

## Proposed Solution

Display refund calculation before cancellation and provide refund tracking.

## Proposed User Flow

1. Open booked ticket.
2. Click Cancel.
3. View refund estimate.
4. Confirm cancellation.
5. Track refund status.

## Technical Implementation Plan

### Components

- Refund API
- Payment Service
- Notification Module

### Data

Refund Record

- Amount
- Status
- Processing Date

### API

GET /refund/status

POST /ticket/cancel

### Frontend

- Refund Timeline
- Refund Calculator

## Success Metrics

- Reduced cancellation confusion
- Increased user trust

## Edge Cases

- Partial cancellation
- Payment gateway delay

---

### Wireframe

![Refund Tracker](../assets/wireframes/refund-tracker.png)


# Feature Spec 6: Mobile Responsive Booking Experience

## Problem Statement

IRCTC mobile website is difficult to use due to small buttons and poor layout.

## Current State

Desktop layout is squeezed into mobile screens.

## Proposed Solution

Create a responsive mobile-first booking experience.

## Proposed User Flow

1. Open website.
2. Login.
3. Search train.
4. View mobile cards.
5. Complete booking.
6. Make payment.

## Technical Implementation Plan

### Components

- Mobile UI
- CSS Framework
- Booking Pages

### Data

No additional database changes.

### API

Existing APIs reused.

### Frontend

- Responsive cards
- Sticky buttons
- Bottom navigation
- Large touch targets

### Third Party

None

## Success Metrics

- Faster booking on mobile
- Lower bounce rate
- Improved accessibility

## Edge Cases

- Small screen devices
- Slow internet
- Orientation changes

### Wireframe

![Mobile Booking](../assets/wireframes/mobile-booking.png)
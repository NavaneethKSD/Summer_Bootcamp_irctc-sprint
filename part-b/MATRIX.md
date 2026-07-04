# Impact vs Effort Matrix

This matrix prioritizes the proposed IRCTC solutions based on their expected user impact and implementation effort.

---

# 2×2 Impact vs Effort Matrix

|                     | **Low Effort** | **High Effort** |
|---------------------|----------------|-----------------|
| **High Impact** | 2. Persistent Smart Search Filters<br>4. Simple PNR Status Dashboard<br>5. Transparent Cancellation & Refund Tracker | 1. Tatkal Virtual Queue System<br>6. Mobile Responsive Booking Experience |
| **Low Impact** | 3. Seat Preference Lock | None |

---

# How I Scored Each Dimension

## Impact (1–5)

Impact was measured using:

- Number of users affected
- Frequency of occurrence
- Whether the issue affects ticket booking
- User frustration level
- Financial or travel consequences

## Effort (1–5)

Effort was measured using:

- Backend changes required
- Database modifications
- API development
- UI redesign
- Infrastructure complexity
- Third-party integrations

---

# Detailed Scores

| Feature | Impact | Effort | Quadrant |
|---------|:------:|:------:|-----------|
| Tatkal Virtual Queue | 5 | 5 | High Impact / High Effort |
| Persistent Smart Search Filters | 5 | 2 | High Impact / Low Effort |
| Seat Preference Lock | 3 | 2 | Low Impact / Low Effort |
| Simple PNR Status Dashboard | 4 | 2 | High Impact / Low Effort |
| Transparent Cancellation & Refund Tracker | 4 | 3 | High Impact / Low Effort |
| Mobile Responsive Booking Experience | 5 | 4 | High Impact / High Effort |

---

# Placement Justifications

## 1. Tatkal Virtual Queue System – High Impact / High Effort

This feature affects millions of Tatkal users every day and directly addresses one of IRCTC's biggest usability issues. It requires backend queue management, database updates, real-time APIs, and notification services, making implementation complex. It should be planned as a major project because of its large impact on booking success.

---

## 2. Persistent Smart Search Filters – High Impact / Low Effort

Many users repeatedly search for trains using the same filters, and filter resets slow down the booking process. Saving filter preferences mainly requires frontend state management and minor backend support, making it relatively easy to implement. This is an excellent quick win that improves usability with limited development effort.

---

## 3. Seat Preference Lock – Low Impact / Low Effort

The issue affects passengers who prefer specific berths, such as lower berths or window seats, but it does not prevent ticket booking. The solution only requires saving seat preferences throughout the booking flow. Since implementation is straightforward but impacts a smaller user group, it is categorized as a fill-in feature.

---

## 4. Simple PNR Status Dashboard – High Impact / Low Effort

Millions of passengers check their PNR status daily, and many are confused by railway abbreviations. Displaying plain-language explanations requires only UI enhancements and minimal backend changes. This feature significantly improves user understanding while requiring relatively little effort.

---

## 5. Transparent Cancellation & Refund Tracker – High Impact / Low Effort

Users frequently cancel tickets and often do not understand refund rules or processing times. Adding refund estimates and tracking mainly involves frontend improvements and integration with existing refund APIs. It is a valuable enhancement that increases user trust without major infrastructure changes.

---

## 6. Mobile Responsive Booking Experience – High Impact / High Effort

A large percentage of IRCTC users access the website from mobile devices, making mobile usability a critical concern. Redesigning the booking flow for responsive layouts requires updates across multiple pages and extensive testing. Although the effort is high, the long-term impact on accessibility and booking completion is substantial.

---

# Recommended Sprint Order

## Sprint 1 – Quick Wins

1. Persistent Smart Search Filters
2. Simple PNR Status Dashboard
3. Transparent Cancellation & Refund Tracker

These features deliver significant improvements with relatively low implementation effort and should be prioritized first.

---

## Sprint 2 – Medium Priority

4. Seat Preference Lock

This feature improves the booking experience for passengers with berth preferences and can be implemented after the quick wins.

---

## Sprint 3 – Major Projects

5. Tatkal Virtual Queue System
6. Mobile Responsive Booking Experience

These initiatives require substantial backend and frontend changes but provide the greatest long-term value for IRCTC users.

---

# Conclusion

Based on the impact and effort analysis, the first development sprint should focus on delivering high-impact, low-effort improvements that quickly enhance the user experience. Larger infrastructure projects such as the Tatkal Virtual Queue and Mobile Responsive Booking Experience should be scheduled as long-term initiatives after foundational improvements have been completed.
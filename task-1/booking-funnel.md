# Booking Funnel Design

## Overview

The booking funnel represents the complete journey a patient follows from visiting the OrthoNow landing page to successfully requesting a consultation. It is designed to measure user engagement, identify conversion opportunities, and analyze drop-off points throughout the booking process.

The funnel will be tracked using **Google Tag Manager (GTM)** and **Google Analytics 4 (GA4)**, enabling detailed insights into user behavior and conversion performance.

---

# Funnel Objective

The primary objective of this funnel is to:

- Measure consultation booking conversions
- Identify user drop-off points
- Improve CTA effectiveness
- Evaluate consultation form completion rate
- Optimize the overall patient booking experience

---

# User Journey

```text
Landing Page
      │
      ▼
View Hero Section
      │
      ▼
Click "Book Free Consultation"
      │
      ▼
Consultation Form Opens
      │
      ▼
User Starts Filling Form
      │
      ▼
Submit Consultation Form
      │
      ▼
Booking Confirmation (Thank You)
```

---

# Funnel Stages

| Stage | User Action | Event Name | Purpose |
|--------|-------------|------------|---------|
| 1 | Landing Page Loaded | `page_view` | Measure website traffic |
| 2 | User clicks "Book Free Consultation" | `consultation_cta_click` | Track CTA engagement |
| 3 | Consultation form becomes visible | `consultation_form_view` | Measure form visibility |
| 4 | User begins entering information | `consultation_form_started` | Measure booking intent |
| 5 | User submits consultation form | `consultation_form_submitted` | Primary conversion event |
| 6 | Thank You message displayed | `consultation_success` | Confirm successful booking |

---

# Funnel Visualization

```text
100% Visitors
      │
      ▼
Landing Page Views
      │
      ▼
CTA Clicks
      │
      ▼
Form Views
      │
      ▼
Form Starts
      │
      ▼
Form Submissions
      │
      ▼
Successful Consultation Requests
```

---

# Key Events

| Event | Description |
|--------|-------------|
| `page_view` | User lands on the website |
| `consultation_cta_click` | User clicks the primary booking button |
| `consultation_form_view` | Consultation form becomes visible |
| `consultation_form_started` | User interacts with the form |
| `consultation_form_submitted` | User successfully submits the form |
| `consultation_success` | Confirmation message is displayed |
| `call_now_click` | User clicks the Call Now button |
| `faq_expand` | User expands an FAQ item |

---

# Primary Conversion

The primary business conversion for this landing page is:

**Consultation Form Submitted**

This event indicates that the user has successfully requested an orthopaedic consultation.

---

# Secondary Conversions

The following interactions provide additional insights into user engagement:

- Book Free Consultation button clicks
- Call Now button clicks
- FAQ interactions
- Consultation form views
- Consultation form starts

---

# Key Performance Indicators (KPIs)

| KPI | Description |
|-----|-------------|
| Landing Page Views | Total visitors reaching the page |
| CTA Click Rate | Percentage of users clicking the consultation button |
| Form Start Rate | Percentage of users beginning the consultation form |
| Form Completion Rate | Percentage of users submitting the form |
| Overall Conversion Rate | Form submissions divided by total visitors |
| Funnel Drop-off Rate | Percentage of users leaving between funnel stages |

---

# Analytics Benefits

Implementing this booking funnel provides valuable business insights, including:

- Identification of high-performing call-to-action buttons
- Analysis of user drop-off before form submission
- Measurement of consultation booking conversions
- Optimization opportunities for user experience
- Better understanding of patient engagement across the booking journey

---

# Implementation Strategy

The funnel events are captured using **Google Tag Manager (GTM)** and forwarded to **Google Analytics 4 (GA4)** through the `dataLayer`.

Each significant user interaction triggers an event that can be analyzed in GA4 Funnel Exploration reports to monitor conversion performance and optimize the consultation booking process.

---

# Expected Funnel Outcome

A successful user journey follows this sequence:

1. User visits the OrthoNow landing page.
2. User reviews orthopaedic services and doctor information.
3. User clicks **Book Free Consultation**.
4. User enters consultation details.
5. User submits the consultation form.
6. User receives a confirmation message.

This completed journey represents the primary conversion tracked for the landing page.

---

# Assumptions

- Each form submission represents one consultation request.
- Users interact with JavaScript-enabled browsers.
- Event tracking is implemented using Google Tag Manager.
- Google Analytics 4 receives all configured events through the dataLayer.
- The landing page is optimized for both desktop and mobile users.

---

# Conclusion

The booking funnel provides a structured approach to measuring user interactions throughout the consultation booking process. By tracking each stage of the patient journey, OrthoNow can identify optimization opportunities, improve conversion rates, and enhance the overall user experience while making data-driven business decisions.
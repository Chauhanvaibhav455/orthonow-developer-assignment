# Task 1 – GTM Event Schema

## Scenario

OrthoNow is a chain of nine orthopaedic clinics operating across Bengaluru, Hyderabad, and Chennai. The primary objective is to implement a comprehensive tracking solution using Google Tag Manager (GTM) and Google Analytics 4 (GA4) to measure user engagement, optimize marketing campaigns, and accurately track consultation bookings across the website.

---

# Approach

The proposed tracking strategy is designed to capture the complete patient journey—from landing on the website to successfully booking a consultation. Each meaningful interaction is tracked as a structured event so that the marketing team can analyze user behavior, identify drop-off points, build remarketing audiences, and optimize advertising campaigns.

Google Tag Manager (GTM) will serve as the central event management layer, while Google Analytics 4 (GA4) will receive and analyze the collected events. Since GTM cannot automatically detect progression within a custom multi-step booking form, the frontend developer will implement custom `window.dataLayer.push()` events after each successful step. GTM will listen for these events and forward them to GA4.

---

# GTM Event Schema

| Event Name                  | Trigger Type                | Key Parameters                                         | GA4 Report / Audience    |
| --------------------------- | --------------------------- | ------------------------------------------------------ | ------------------------ |
| consultation_form_start     | Form Visibility Trigger     | page_url, campaign_name, device_type                   | Funnel Exploration       |
| booking_step_complete       | Custom Event (dataLayer)    | step_number, step_name, clinic_location, specialty     | Funnel Exploration       |
| booking_completed           | Custom Event (dataLayer)    | booking_id, clinic_location, specialty, booking_status | Conversions              |
| call_now_click              | Click Trigger               | button_location, clinic_name, page_url                 | Engagement Report        |
| whatsapp_click              | Click Trigger               | page_url, device_type, source_page                     | Lead Engagement Audience |
| patient_guide_download      | Form Submit + File Download | guide_name, phone_number, page_url                     | Lead Magnet Report       |
| clinic_page_view            | Page View Trigger           | clinic_name, city, page_url                            | Content Report           |
| blog_scroll_50              | Scroll Depth Trigger (50%)  | article_title, scroll_percent, page_url                | Engaged Users            |
| blog_scroll_90              | Scroll Depth Trigger (90%)  | article_title, scroll_percent, reading_time            | High Intent Readers      |
| consultation_form_submitted | Custom Event                | patient_name, phone_number, campaign_name              | Conversion Report        |

### Scroll Tracking Strategy

Two scroll-depth events are implemented for blog articles:

* **50% Scroll** – Indicates meaningful engagement with the content.
* **90% Scroll** – Indicates the article has been read almost completely and can be used to build a high-intent audience for remarketing.

---

# Booking Funnel Tracking

The appointment booking process consists of three steps.

Because this is a custom multi-step form, Google Tag Manager cannot detect user progression automatically. The frontend developer is responsible for implementing `window.dataLayer.push()` events whenever a user successfully completes a step. GTM listens for these custom events and forwards them to GA4, enabling detailed funnel analysis and conversion tracking.

---

## Step 1 – Select Clinic Location & Specialty

**User Action**

* Select Clinic Location
* Select Orthopaedic Specialty

**GTM Trigger**

Custom Event → `booking_step_complete`

```javascript
window.dataLayer = window.dataLayer || [];

window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 1,
  step_name: "location_specialty_selected",
  clinic_location: "Bengaluru - Indiranagar",
  specialty: "Knee Replacement"
});
```

---

## Step 2 – Enter Patient Details

**User Action**

* Enter Name
* Enter Phone Number
* Select Preferred Consultation Date

**GTM Trigger**

Custom Event → `booking_step_complete`

```javascript
window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 2,
  step_name: "patient_information_entered",
  patient_name: "Rahul Sharma",
  phone_number: "9876543210",
  preferred_date: "2026-07-05",
  clinic_location: "Bengaluru - Indiranagar"
});
```

---

## Step 3 – Confirm Booking

**User Action**

* Review Details
* Confirm Appointment

**GTM Trigger**

Custom Event → `booking_step_complete`

```javascript
window.dataLayer.push({
  event: "booking_step_complete",
  step_number: 3,
  step_name: "booking_confirmed",
  clinic_location: "Bengaluru - Indiranagar",
  specialty: "Knee Replacement",
  booking_status: "Confirmed"
});
```

---

## Final Booking Success Event

After the appointment is successfully created in the backend, a separate conversion event is pushed.

```javascript
window.dataLayer.push({
  event: "booking_completed",
  booking_id: "BK10234",
  clinic_location: "Bengaluru - Indiranagar",
  specialty: "Knee Replacement",
  booking_status: "Confirmed"
});
```

---

# Funnel Drop-off Analysis

The following events will be configured inside **GA4 Funnel Exploration**.

| Funnel Step               | GA4 Event                               |
| ------------------------- | --------------------------------------- |
| Landing Page Viewed       | page_view                               |
| Consultation Form Started | consultation_form_start                 |
| Step 1 Completed          | booking_step_complete (step_number = 1) |
| Step 2 Completed          | booking_step_complete (step_number = 2) |
| Step 3 Completed          | booking_step_complete (step_number = 3) |
| Booking Completed         | booking_completed                       |

This funnel allows the marketing team to identify where users abandon the booking process.

Example:

* If users leave after Step 1, the clinic or specialty selection may be confusing.
* If users leave after Step 2, the personal information form may be too long or difficult to complete.
* If users leave after Step 3, there may be technical issues during booking confirmation.

These insights help improve the booking experience and increase conversion rates.

---

# GA4 Funnel Exploration

A GA4 Funnel Exploration report will be created using the events defined above. This report visualizes the complete patient journey from landing on the website to successfully booking a consultation.

The funnel enables the team to:

* Measure completion rates for each booking step.
* Identify the stage with the highest abandonment rate.
* Compare conversion performance across clinic locations.
* Analyze differences between desktop and mobile users.
* Evaluate campaign performance by traffic source.

These insights allow both the marketing and product teams to make data-driven improvements to the booking experience.

---

# Google Ads Conversion

## Selected Conversion Event

**booking_completed**

### Why this event?

The **booking_completed** event represents a successful consultation booking, making it the most valuable business outcome.

Importing this event into Google Ads allows automated bidding strategies such as **Maximize Conversions** and **Target CPA** to optimize campaigns toward actual appointment bookings instead of intermediate interactions.

Although events such as **Call Now**, **WhatsApp Click**, and **Patient Guide Download** indicate user interest, they do not guarantee that a consultation has been booked. Therefore, using **booking_completed** as the primary Google Ads conversion provides the highest-quality optimization signal and improves return on ad spend (ROAS).

All remaining events continue to be collected in GA4 for engagement reporting, audience creation, funnel analysis, and remarketing.

# Google Tag Manager (GTM) Event Schema

## Overview

This document defines the Google Tag Manager (GTM) event tracking implementation for the **OrthoNow Consultation Landing Page**.

The objective is to capture meaningful user interactions throughout the consultation booking journey and send structured event data to **Google Analytics 4 (GA4)** for reporting, conversion tracking, and funnel analysis.

---

# Tracking Strategy

The tracking implementation focuses on measuring the complete patient journey, from arriving on the landing page to successfully requesting a consultation.

Events are pushed into the **dataLayer**, captured by **Google Tag Manager**, and forwarded to **Google Analytics 4**.

```
User Interaction
        │
        ▼
   dataLayer.push()
        │
        ▼
Google Tag Manager
        │
        ▼
Google Analytics 4
        │
        ▼
Reports • Conversions • Funnel Exploration
```

---

# Event Schema

| Event Name | Trigger | Event Category | Parameters | Purpose |
|------------|----------|----------------|------------|---------|
| `page_view` | Landing page loads | Engagement | page_title, page_location | Track website visitors |
| `consultation_cta_click` | User clicks **Book Free Consultation** | Conversion | button_text, section | Measure CTA engagement |
| `call_now_click` | User clicks **Call Now** | Engagement | phone_number | Track phone enquiries |
| `consultation_form_view` | Consultation form becomes visible | Engagement | form_name | Measure form visibility |
| `consultation_form_started` | User enters first form field | Engagement | field_name | Measure booking intent |
| `consultation_form_submitted` | Consultation form submitted | Conversion | patient_name, phone_number, source | Primary conversion |
| `consultation_success` | Thank-you message displayed | Conversion | booking_status | Successful booking |
| `faq_expand` | FAQ item expanded | Engagement | question_title | Track FAQ interactions |

---

# Event Parameters

| Parameter | Type | Description |
|------------|------|-------------|
| patient_name | String | Name entered by the user |
| phone_number | String | Contact number entered by the user |
| source | String | Source page or campaign |
| button_text | String | CTA button label |
| section | String | Section where interaction occurred |
| booking_status | String | Booking outcome |
| question_title | String | FAQ question expanded |
| form_name | String | Name of the consultation form |
| field_name | String | First form field interacted with |

---

# Sample dataLayer Events

## 1. CTA Button Click

```javascript
window.dataLayer.push({
  event: "consultation_cta_click",
  button_text: "Book Free Consultation",
  section: "Hero"
});
```

---

## 2. Consultation Form Started

```javascript
window.dataLayer.push({
  event: "consultation_form_started",
  field_name: "Full Name"
});
```

---

## 3. Consultation Form Submitted

```javascript
window.dataLayer.push({
  event: "consultation_form_submitted",
  patient_name: "Rahul Sharma",
  phone_number: "9876543210",
  source: "Consultation Landing Page"
});
```

---

## 4. Call Now Button

```javascript
window.dataLayer.push({
  event: "call_now_click",
  phone_number: "+91XXXXXXXXXX"
});
```

---

## 5. FAQ Interaction

```javascript
window.dataLayer.push({
  event: "faq_expand",
  question_title: "Do I need a referral before booking?"
});
```

---

# GTM Trigger Configuration

| Trigger Name | Trigger Type | Fires On |
|--------------|-------------|----------|
| Page View | Page View | Landing page load |
| CTA Click | Click Trigger | Book Consultation button |
| Call Button Click | Click Trigger | Call Now button |
| Form View | Element Visibility | Consultation form |
| Form Started | Custom Event | First user interaction |
| Form Submitted | Form Submission / Custom Event | Successful form submission |
| FAQ Click | Click Trigger | FAQ accordion |

---

# GA4 Event Mapping

| GTM Event | GA4 Event | Conversion |
|------------|-----------|------------|
| page_view | page_view | No |
| consultation_cta_click | consultation_cta_click | No |
| call_now_click | call_now_click | No |
| consultation_form_view | consultation_form_view | No |
| consultation_form_started | consultation_form_started | No |
| consultation_form_submitted | consultation_form_submitted | **Yes** |
| consultation_success | consultation_success | **Yes** |
| faq_expand | faq_expand | No |

---

# Recommended GA4 Conversions

The following events should be marked as conversions in Google Analytics 4:

- consultation_form_submitted
- consultation_success

These events represent successful consultation requests and are the primary business goals of the landing page.

---

# Analytics Use Cases

The collected data enables the following analyses:

- Landing page traffic analysis
- CTA click-through rate (CTR)
- Consultation booking conversion rate
- Form abandonment analysis
- Funnel drop-off identification
- FAQ engagement tracking
- Call button interaction analysis

---

# Implementation Notes

- All events follow **GA4 snake_case naming conventions**.
- Events are pushed through the **dataLayer**.
- GTM captures the events and forwards them to **Google Analytics 4**.
- Personally identifiable information (PII) should not be sent to GA4 in a production environment. The example values shown in this assignment are for demonstration purposes only.
- Event names and parameters are designed to be scalable for future enhancements such as appointment scheduling, doctor selection, and payment integration.

---

# Event Flow Summary

```
Landing Page
      │
      ▼
CTA Click
      │
      ▼
Consultation Form
      │
      ▼
Form Started
      │
      ▼
Form Submitted
      │
      ▼
Thank You Screen
      │
      ▼
GA4 Conversion Recorded
```

---

# Conclusion

The GTM event schema provides a structured and scalable tracking framework for the OrthoNow consultation landing page. By capturing each key interaction and forwarding standardized events to Google Analytics 4, the implementation enables accurate funnel analysis, conversion measurement, and data-driven optimization of the patient booking experience.
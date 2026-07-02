# Task 3 – GTM & GA4 Integration Design

## Project Overview

OrthoNow is a healthcare provider with multiple orthopaedic clinics across South India. The objective of this implementation is to design a scalable analytics architecture using Google Tag Manager (GTM) and Google Analytics 4 (GA4) to accurately track user interactions throughout the consultation booking journey.

The solution captures meaningful user actions such as consultation form submissions, booking progress, phone calls, WhatsApp interactions, clinic page visits, downloads, and content engagement. These events help the marketing team understand user behavior, optimize campaigns, and improve conversion rates.

---

# Architecture Overview

```
                         User
                           │
                           ▼
               OrthoNow Landing Page
                 (HTML, CSS, JavaScript)
                           │
                           ▼
               window.dataLayer.push()
                           │
                           ▼
                Google Tag Manager (GTM)
                           │
        ┌──────────────────┴──────────────────┐
        ▼                                     ▼
 GA4 Event Tags                      Google Ads Conversion Tag
        │                                     │
        ▼                                     ▼
 Google Analytics 4                 Google Ads Conversion Tracking
        │
        ▼
Reports, Funnel Exploration,
Audience Building & Engagement Analysis
```

---

# Tracking Workflow

The complete tracking workflow consists of the following steps.

### Step 1 – User Interaction

The visitor interacts with the landing page.

Examples include:

- Opening a clinic page
- Clicking "Call Now"
- Clicking WhatsApp
- Starting the consultation form
- Completing booking steps
- Successfully submitting the consultation request

---

### Step 2 – JavaScript Event

Whenever an important interaction occurs, JavaScript pushes a structured event into the browser's `window.dataLayer`.

Example:

```javascript
window.dataLayer.push({
    event: "consultation_form_submitted",
    patient_name: "Rahul Sharma",
    phone_number: "9876543210",
    source: "Landing Page"
});
```

The `dataLayer` acts as the communication bridge between the website and Google Tag Manager.

---

### Step 3 – Google Tag Manager

Google Tag Manager continuously listens for custom events.

When an event such as

```
consultation_form_submitted
```

is detected, GTM fires the corresponding trigger.

Example:

```
Custom Event Trigger

Event Name:
consultation_form_submitted
```

---

### Step 4 – GA4 Event Tag

The GTM trigger activates a GA4 Event Tag.

The following information is sent to Google Analytics 4.

Example parameters:

- patient_name
- phone_number
- source
- clinic_location
- specialty
- booking_status

These parameters become available inside GA4 reports.

---

### Step 5 – Google Analytics 4

GA4 stores every event and makes it available for reporting.

Examples include:

- Funnel Exploration
- Engagement Report
- Conversion Report
- Landing Page Analysis
- User Journey Analysis

Marketing teams can then analyze:

- Conversion Rate
- Funnel Drop-offs
- User Engagement
- Campaign Performance
- High Performing Clinics

---

### Step 6 – Google Ads Conversion Tracking

Important conversion events can also be forwarded to Google Ads.

Example:

```
booking_completed
```

or

```
consultation_form_submitted
```

These conversions help optimize paid advertising campaigns and improve return on ad spend (ROAS).

---

# Event Tracking Architecture

| User Interaction | dataLayer Event | GTM Trigger | GA4 Event |
|------------------|-----------------|------------|------------|
| Consultation Form Submitted | consultation_form_submitted | Custom Event | consultation_form_submitted |
| Booking Step Completed | booking_step_complete | Custom Event | booking_step_complete |
| Booking Completed | booking_completed | Custom Event | booking_completed |
| Call Now Button | call_now_click | Click Trigger | call_now_click |
| WhatsApp Click | whatsapp_click | Click Trigger | whatsapp_click |
| Patient Guide Download | patient_guide_download | File Download Trigger | patient_guide_download |
| Clinic Page Viewed | clinic_page_view | Page View Trigger | clinic_page_view |
| Blog Scroll 50% | blog_scroll_50 | Scroll Trigger | blog_scroll_50 |
| Blog Scroll 90% | blog_scroll_90 | Scroll Trigger | blog_scroll_90 |

---

# GA4 Reports

The collected events support multiple GA4 reports.

| Event | GA4 Report |
|--------|------------|
| booking_step_complete | Funnel Exploration |
| booking_completed | Conversions |
| consultation_form_submitted | Conversion Report |
| clinic_page_view | Pages & Screens |
| blog_scroll_50 | Engagement Report |
| blog_scroll_90 | Engaged Users |
| call_now_click | Engagement |
| whatsapp_click | Lead Engagement |

---

# Funnel Exploration

The booking journey can be visualized inside GA4 Funnel Exploration.

```
Landing Page
      │
      ▼
Consultation Form Started
      │
      ▼
Booking Step 1
(Location & Specialty)
      │
      ▼
Booking Step 2
(Patient Details)
      │
      ▼
Booking Step 3
(Confirmation)
      │
      ▼
Booking Completed
```

This report helps identify where users abandon the booking process.

Example insights:

- Users leaving after Step 1
- Users dropping during patient information
- Successful booking completion rate

---

# Why Google Tag Manager?

Google Tag Manager provides several advantages.

- Centralized tag management
- No need to modify application code for every tracking change
- Easy deployment of new analytics events
- Better collaboration between developers and marketers
- Reduced development effort
- Faster implementation of marketing tags

---

# Why use dataLayer?

The `window.dataLayer` object provides a standardized method of sending structured information from the website to GTM.

Instead of embedding analytics code throughout the application, developers simply push structured events into the dataLayer.

Benefits include:

- Decouples analytics from application logic
- Easier maintenance
- Cleaner JavaScript code
- Supports multiple analytics platforms
- More reliable event tracking

---

# Scalability

The proposed architecture is designed to support future enhancements without modifying the existing tracking framework.

Possible future additions include:

- Doctor profile tracking
- Appointment cancellation tracking
- Payment success events
- Video consultation events
- Patient portal interactions
- AI chatbot engagement
- CRM integration
- Meta Pixel integration
- Microsoft Clarity
- LinkedIn Insight Tag

---

# Benefits of the Solution

The implemented GTM + GA4 architecture provides several business advantages.

- Complete patient journey tracking
- Accurate conversion measurement
- Better campaign attribution
- Improved marketing optimization
- Enhanced user behavior analysis
- Scalable event management
- Reduced maintenance effort
- Future-ready analytics implementation

---

# Conclusion

The proposed integration provides a scalable, maintainable, and production-ready analytics architecture for OrthoNow.

Google Tag Manager acts as the central event management layer, while Google Analytics 4 provides detailed reporting on user behavior, engagement, and conversions. Custom `window.dataLayer.push()` events enable accurate tracking of the complete consultation booking journey without tightly coupling analytics code with the application.

This architecture allows the marketing team to measure conversion performance, optimize campaigns, identify funnel drop-offs, and continuously improve the patient booking experience.
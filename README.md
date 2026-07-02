# OrthoNow - Developer & Martech Assignment

This repository contains the production code layout and tracking schema designed for OrthoNow's digital growth ecosystem.

---

## 📊 Task 01 - GTM Event Schema

### 1. Full Event Tracking Grid
Below is the systematic layout of interactions required before going live:

| Event Name | Trigger Type | Key Parameters (Min. 3) | GA4 Report Target / Destination |
| :--- | :--- | :--- | :--- |
| `booking_step_complete` | Custom Event | `step_number`, `step_name`, `clinic_location`, `specialty` | Explore > Funnel Exploration |
| `appointment_booked` | Custom Event | `booking_id`, `clinic_location`, `specialty`, `preferred_date` | Engagement > Conversions |
| `click_to_call` | Just Links | `click_url`, `link_text`, `page_location` | Engagement > Events |
| `whatsapp_chat_initiate` | Just Links | `click_url`, `wa_link_domain`, `page_location` | Engagement > Events |
| `patient_guide_gated_submit`| Custom Event | `form_name`, `file_name`, `page_location` | Engagement > Conversions |
| `clinic_location_view` | Page View | `page_location`, `clinic_name`, `city_region` | Engagement > Pages and screens |
| `blog_scroll_depth` | Scroll | `scroll_threshold`, `page_title`, `article_category` | Engagement > Events |

### 2. Multi-Step Funnel Mapping via JSON DataLayers
Since GTM cannot inherently monitor step transitions natively without standard front-end pushes, the following programmatic pushes will fire at each state:

#### Step 1: Location & Specialty Selected
```json
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'booking_step_complete',
  'step_number': 1,
  'step_name': 'location_specialty_selected',
  'clinic_location': 'Indiranagar',
  'specialty': 'Orthopaedic Surgery'
});
#### Step 2: Contact Information Input Filled
```json
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'booking_step_complete',
  'step_number': 2,
  'step_name': 'contact_details_entered',
  'clinic_location': 'Indiranagar',
  'specialty': 'Orthopaedic Surgery'
});
window.dataLayer = window.dataLayer || [];
window.dataLayer.push({
  'event': 'appointment_booked',
  'step_number': 3,
  'step_name': 'booking_confirmed',
  'clinic_location': 'Indiranagar',
  'specialty': 'Orthopaedic Surgery',
  'booking_id': 'ORTHO-78419'
});    

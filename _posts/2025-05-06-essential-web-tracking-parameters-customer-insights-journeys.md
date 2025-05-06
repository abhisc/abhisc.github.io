---

title: "Essential Web Tracking Parameters for Customer Insights – Journeys"
date: 2025-05-06
tags: \[tracking, marketing, crm, dynamics365, customer-insights, realtime-journeys]
categories: \[Marketing, CRM, Dynamics365]
layout: post
------------

When running digital campaigns, capturing **UTM parameters** like `utm_source` and `utm_campaign` is a common and essential practice. But that’s just the tip of the iceberg. There’s a lot more you can (and should) track to enrich journeys and drive personalized experiences, and this can also be achieved on **Dynamics 365 Customer Insights – Journeys (real-time marketing)**,

In this post, we’ll walk through:

* What else you can capture beyond UTM
* How it enhances Customer Insights – Journeys
* A structured table of what data to collect and how
* For Further Exploration: Recommended Posts on Advanced UTM and Parameter Tracking

---

## 🌐 What You Can Capture (Beyond UTM)

| Category              | Data Point                                                            | How to Capture                            |
| --------------------- | --------------------------------------------------------------------- | ----------------------------------------- |
| **Campaign Metadata** | `utm_source`, `utm_medium`, `utm_campaign`, `utm_term`, `utm_content` | From URL parameters via JavaScript        |
| **Referral Info**     | Referrer URL                                                          | `document.referrer`                       |
| **Landing Page Info** | Full URL                                                              | `window.location.href`                    |
| **Timestamp**         | Visit time                                                            | `new Date().toISOString()` or server log  |
| **Geolocation**       | Country, region, city, IP                                             | IP-based lookup API (e.g., ipapi, ipinfo) |
| **Device Info**       | OS, device, browser                                                   | `navigator.userAgent`, use `bowser.js`    |
| **Screen Info**       | Resolution, size                                                      | `screen.width`, `screen.height`           |
| **Language**          | Browser language                                                      | `navigator.language`                      |
| **Returning Visitor** | Yes/No                                                                | Cookies or `localStorage`                 |
| **Session ID**        | Unique session                                                        | Generate UUID and store locally           |
| **Engagement**        | Time on page, scroll                                                  | JS timers + scroll listeners              |
| **Click Path**        | Page navigation                                                       | Track via session history or logs         |
| **Form Abandonment**  | Partial fills                                                         | Field-level tracking events               |

---

## 🤔 Why It Matters in Customer Insights – Journeys

In the context of **real-time journeys**, this additional data powers:

* **Enhanced Segmentation:** Create segments based on campaign, geography, or user behavior.
* **Journey Triggers:** Start a journey when someone clicks a specific UTM-tracked link or visits via a referral source.
* **Dynamic Branching:** Use captured data like `utm_source`, location, or device type to personalize paths.
* **Deeper Analytics:** Understand what content resonates, which sources convert, and how visitors engage.
* **Better Attribution:** Referrer URLs and UTM combinations provide full-funnel visibility.

> For example, a journey could be triggered when someone visits from Instagram (utm\_source) and uses a mobile device — prompting an SMS-based follow-up instead of email.

These insights make your real-time journeys more targeted, contextual, and ultimately more successful.

---

## 🔧 How to Capture This in Customer Insights – Journeys

To implement this tracking in **Dynamics 365 Customer Insights – Journeys**, follow these key steps:

1. **Marketing Forms**: Use real-time marketing forms as the main method for capturing visitor data. These forms support both mapped and unmapped fields.

2. **Hidden Fields**: Add hidden input fields to your form for `utm_source`, `utm_campaign`, `referrer`, and other tracking parameters. These fields won't be visible to the user but will be populated and submitted along with the form.

3. **JavaScript Injection**:

   * Use a small script to extract values from the URL (like UTM parameters).
   * Use `document.referrer` to capture where the visitor came from.
   * Populate the hidden fields programmatically before the form is submitted.

4. **Store in CRM**: Map these form fields to custom attributes on the Contact or Lead table. Even if fields are not mapped, they can still be viewed later for analysis.

5. **Use in Journeys**:

   * Use captured data as filters or triggers in real-time journeys.
   * For example, launch a different branch of a journey if `utm_source = instagram` or if `device = mobile`.

This setup ensures you’re not just capturing form submissions — you’re building rich context around every interaction.

### 📥 Example: Additional Fields in Form Submission

You could send these extra values to Dynamics CRM fields like:

* `entry_url`
* `device_type`
* `browser_name`
* `ip_country`
* `first_touch_timestamp`

All of these can be created as custom fields on a **Lead** or **Contact** record.

---

## 📚 References & Credits

Here are some excellent resources from the community that go deeper into specific aspects:

* [Capturing UTM Parameters via Real-Time Marketing (Megan V. Walker)](https://meganvwalker.com/capturing-utm-parameters-via-realtime-marketing/)
* [Use Unmapped Form Fields to Capture the Referral URL (Megan V. Walker)](https://meganvwalker.com/use-unmapped-form-field-capture-referral-url/)
* [How to Capture the Referrer URL in Dynamics 365 Marketing (Amey Holden)](https://www.ameyholden.com/articles/dynamics-365-marketing-form-referre-url)
* [Measure marketing effectiveness using UTM codes (MS Learn)](https://learn.microsoft.com/en-us/dynamics365/customer-insights/journeys/real-time-marketing-utm)


These posts are packed with practical advice and step-by-step guides.

---

**Further Considerations:** 

>Exploring a Separate Web Visit Entity: While storing web visit data in a dedicated custom entity like "Web Visit" offers cleaner tracking and more robust reporting, it certainly involves additional implementation.

>To what extent can we leverage custom JavaScript within Customer Insights - Journeys forms in this process?

Happy tracking!

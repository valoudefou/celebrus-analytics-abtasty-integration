# AB Tasty → Celebrus Integration
## Overview

This integration captures AB Tasty experiment exposures and pushes them to the **Celebrus Data Collection platform** using template variables. It is designed for use in tag managers or other environments where AB Tasty template variables are available (`{{campaignId}}`, `{{campaignName}}`, etc.).

---

## Prerequisites

- AB Tasty implemented with template variables accessible in your environment.  
- Celebrus **Data Collection for HTML5** library loaded (`window.CelebrusEQ` available).  
- Basic knowledge of JavaScript or tag manager usage.

---

## Template Variables

| Variable          | Description                           | Example                          |
|------------------|---------------------------------------|----------------------------------|
| `{{campaignId}}`    | AB Tasty experiment ID                | `12345`                          |
| `{{campaignName}}`  | AB Tasty experiment name              | `"Homepage Hero Test"`           |
| `{{variationId}}`   | AB Tasty variant bucket ID            | `B`                              |
| `{{variationName}}` | AB Tasty variant display name         | `"Variant B"`                    |
| `timestamp`      | ISO timestamp of exposure              | `"2025-10-14T09:25:00Z"`        |

---

## Implementation Snippet

Insert the following code wherever both AB Tasty template variables and Celebrus library are available:

```javascript
window.CelebrusEQ.send('ABTasty', {
  campaignId: {{campaignId}},
  campaignName: {{campaignName}},
  variationId: {{variationId}},
  variationName: {{variationName}},
  timestamp: new Date().toISOString()
});
```

**Notes:**

- The `{{campaignId}}`, `{{campaignName}}`, `{{variationId}}`, and `{{variationName}}` placeholders are replaced at runtime by your tag manager or AB Tasty template engine.  
- `window.CelebrusEQ.send` sends the data directly into the Celebrus event queue.  
- `timestamp` ensures every event includes the precise time of exposure.

---

## Data Flow Diagram

```text
+----------------+         +----------------+         +------------------+
|                |         |                |         |                  |
| AB Tasty       |  ---->  | Tag Manager /  |  ---->  | Celebrus EQ JS   |
| Template Vars  |         | Custom HTML    |         | (window.CelebrusEQ)|
| {{campaignId}} |         | Snippet        |         |                  |
| {{variationId}}|         |                |         |                  |
+----------------+         +----------------+         +------------------+
        |                         |                           |
        |                         |                           |
        |------------------------->-------------------------->|
                         Data pushed in real-time
```

---

## Optional Enhancements

- Add **consent checks** to ensure events are only sent when the visitor has granted permission.  
- Include additional **custom attributes** as needed for richer analytics.  
- Use **dataLayer forwarding** if the same payload should be captured in other analytics platforms.

---

## Outcome

- Every AB Tasty experiment exposure is captured in Celebrus in real-time.  
- Template-based integration ensures non-developers can deploy this snippet quickly.  
- Enables cross-platform analytics, reporting, and personalization based on experiment participation.

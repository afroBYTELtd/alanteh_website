# Africa Solar Mobility public website V12

Launch ready public company website for Africa Solar Mobility.

Public pages:
- Home
- Ride Service
- Energy Hubs
- Partners
- About
- Contact
- Privacy
- Terms

The public website is intentionally simple. It presents Africa Solar Mobility as a clean mobility and energy operations company serving Ghana first. Private project details belong in internal documents, the Command Center, and private data rooms, not on the public site.

Task 46C wires the Ride Service, Energy Hubs, Partners, and Contact forms to the approved Command Center public enquiry intake path: `/dashboard/public-enquiry/`. The forms submit only public-safe enquiry fields and do not expose internal Command Center workflow fields.

Task 46D adds a lightweight honeypot safety field named `website_url` to the Ride Service, Energy Hubs, Partners, and Contact enquiry forms. The field is hidden from normal visitors, is not saved as enquiry data, and helps the backend ignore bot-like submissions while preserving the approved public-safe form contract.

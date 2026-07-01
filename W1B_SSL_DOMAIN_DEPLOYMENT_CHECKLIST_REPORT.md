# W1B — SSL, Domain, and Deployment Checklist Report

## Status

W1B is partially verified from the website package, but live deployment cannot be completed or accepted from this environment because DNS, hosting, SSL, live server, and Control Center access were not provided.

This report does not claim that the live public website is deployed. It documents the checks completed locally and the exact live-access items still required.

## Starting baseline

Accepted W1A website package:

```text
africa-solar-mobility-public-website-taskW1A-static-429-handling-correction.zip
SHA-256: bcb6d557e16d1f6afa79a551673bbf007f08e29c138eeba73a83403a44b1cd5e
```

## Live domain identified from package

The package references this public domain in `robots.txt` and `sitemap.xml`:

```text
https://africasolarmobility.com/
```

## Local package verification completed

### All 8 public pages are present

```text
index.html: PASS
ride-service.html: PASS
energy-hubs.html: PASS
partners.html: PASS
about.html: PASS
contact.html: PASS
privacy.html: PASS
terms.html: PASS
```

### All 8 public pages load through a local static server

Command pattern used:

```text
python -m http.server 8765
curl -s -o /dev/null -w '%{http_code}' http://127.0.0.1:8765/<page>
```

Result:

```text
/: 200
/ride-service.html: 200
/energy-hubs.html: 200
/partners.html: 200
/about.html: 200
/contact.html: 200
/privacy.html: 200
/terms.html: 200
/robots.txt: 200
/sitemap.xml: 200
```

### robots.txt and sitemap.xml are present locally

```text
robots.txt: PASS
sitemap.xml: PASS
```

### Navigation and local internal links

Static internal navigation link check:

```text
Internal links across all 8 public pages: PASS
Referenced local assets: PASS
```

### Enquiry form contract

The four public enquiry forms remain present on:

```text
ride-service.html
energy-hubs.html
partners.html
contact.html
```

Each form still uses:

```text
action="/dashboard/public-enquiry/"
method="post"
```

Result:

```text
Form endpoint preserved on all four forms: PASS
Form field names preserved: PASS
website_url honeypot present on all four forms: PASS
website_url honeypot hidden with off-screen label, aria-hidden, and tabindex=-1: PASS
```

### Website-side W1A JavaScript still passes static checks

```text
fetch('/dashboard/public-enquiry/'): PASS
HTTP 429 clean message: PASS
Network failure message: PASS
Safe success message: PASS
No missing /thank-you.html redirect: PASS
JavaScript syntax check with node --check: PASS
```

## Live deployment checks that could not be completed

The following W1B acceptance checks require live DNS/hosting/SSL/Control Center access and were not possible from the provided static package alone:

```text
DNS A record or CNAME configuration: NOT COMPLETED
SSL certificate installation: NOT COMPLETED
HTTP to HTTPS redirect on live domain: NOT COMPLETED
All 8 public pages tested on live HTTPS domain: NOT COMPLETED
Live enquiry form submission: NOT COMPLETED
Control Center enquiry record confirmation: NOT COMPLETED
Live robots.txt URL verification: NOT COMPLETED
Live sitemap.xml URL verification: NOT COMPLETED
Live broken-link crawl on deployed domain: NOT COMPLETED
```

Attempted domain check from the execution environment:

```text
curl -I https://africasolarmobility.com/
Result: Could not resolve host: africasolarmobility.com

curl -I http://africasolarmobility.com/
Result: Could not resolve host: africasolarmobility.com
```

Because the domain could not be resolved and no DNS or hosting credentials were provided, the deployment work must not be marked complete.

## Access required to complete W1B

To complete W1B, the developer needs:

```text
1. Domain registrar or DNS provider access for africasolarmobility.com
2. Hosting provider or server access for the public website
3. SSL certificate controls or provider-managed SSL access
4. Deployment path for the accepted W1A website ZIP
5. Control Center environment connected to /dashboard/public-enquiry/
6. Staff access to verify the live enquiry record after a real submission
7. Previous accepted deployment/archive location for rollback
```

## Rollback plan draft

This rollback plan is prepared but must be confirmed by the hosting provider/server operator.

### Rollback trigger

Rollback if any of the following occur after deployment:

```text
- HTTPS fails or certificate is invalid
- HTTP does not redirect to HTTPS
- Any of the 8 public pages fails to load
- Navigation links break
- robots.txt or sitemap.xml is unavailable
- Enquiry form does not create a Control Center enquiry
- The live deployment exposes backend/debug/internal errors
```

### Rollback source

Use the previous accepted public website archive stored by the PM/deployment owner. Current known accepted pre-W1B website package:

```text
africa-solar-mobility-public-website-taskW1A-static-429-handling-correction.zip
SHA-256: bcb6d557e16d1f6afa79a551673bbf007f08e29c138eeba73a83403a44b1cd5e
```

### Rollback action

Depending on hosting setup, perform one of these approved rollback actions:

```text
Static host/provider-managed deployment:
- Re-deploy the previous accepted ZIP/archive from the hosting dashboard.
- Confirm the deployed version matches the previous accepted archive.

Server/SFTP deployment:
- Move the current deployed web root to a timestamped backup directory.
- Restore the previous accepted website files to the web root.
- Restart or reload the web server only if required by the host.

Git-based deployment:
- Revert the deployment commit to the previous accepted tag/commit.
- Trigger a clean redeploy.
```

### Rollback verification

After rollback:

```text
- Confirm HTTPS loads.
- Confirm HTTP redirects to HTTPS.
- Confirm all 8 public pages return 200.
- Confirm robots.txt and sitemap.xml return 200.
- Confirm enquiry form still posts to /dashboard/public-enquiry/.
- Confirm no internal/debug details are visible.
```

## Scope confirmation

```text
No new public website feature added.
No new page added.
No navigation item added.
No booking added.
No payment added.
No login added.
No GPS or map added.
No driver portal added.
No customer dashboard added.
No internal Control Center link added.
No CAPTCHA added.
No W1C, W1D, Phase 2, or go-live task started.
```

## W1B acceptance status

```text
W1B: BLOCKED / NOT ACCEPTED YET
Reason: Live DNS, SSL, hosting, deployment, and Control Center verification access are required.
```

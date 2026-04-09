## BUG-001: Trips API returns empty list → booking unavailable
### Title:
Trips API returns empty response → no routes available for booking
### Environment:
Staging: https://acp-front-nu.vercel.app
API: https://acp-api-w2ng.onrender.com
Browser: Chrome 146.0.7680.165
Date: 03.04.2026
### Preconditions:
User opens homepage
Application successfully loads
API requests are sent to backend
### Steps to reproduce:
Open homepage
Open DevTools → Network
Filter by Fetch/XHR
Find request: /api/v1/trips
Open Response / Preview
Check returned data
Try to select route on UI
### Actual result:
/trips request returns 200 OK
Response body is empty array ([])
UI displays message: "Наразі немає доступних маршрутів"
Route dropdown is disabled
Time dropdown is disabled
User cannot proceed with booking
### Expected result:
/trips should return list of available routes
UI should display routes in dropdown
User should be able to select route and time
Booking flow should be available
### Priority:High
### Severity:
🔴 Critical (core business flow is blocked)
### Notes:
No 500 errors observed
API responds successfully but without data
Issue may be caused by:
missing test data on backend
incorrect filtering logic
environment misconfiguration


## BUG-002: Incorrect error message when Trips API fails
### Title:
Incorrect error message displayed when Trips API request fails
### Environment:
Frontend: https://acp-front-nu.vercel.app
API: https://acp-api-w2ng.onrender.com
Browser: Chrome 146.0.7680.165
Date: 05.04.2026
### Preconditions:
User opens the homepage
Application loads successfully
### Steps to reproduce:
1. Open the website
2. Open DevTools (F12)
3. Go to Network tab
4. Find request to /api/v1/trips or /users/profile
5. Right-click on request → Block request URL
6. Refresh the page
### Actual result:
When API request fails (blocked), UI displays message:
"Наразі немає доступних маршрутів" (No routes available)
This message is misleading because the issue is caused by API failure, not absence of data.
### Expected result:
User should see an appropriate error message indicating a server or network issue (e.g. "Failed to load data", "Server error", etc.)
UI should clearly communicate that data could not be loaded due to an error.
### Priority: High
### Severity: Medium
### Attachments:
### Screenshots showing:
- Blocked request in Network tab
- UI displaying incorrect message.

## BUG-003: Header overlaps content when scrolling
### Title:
Header overlaps page content during scroll, causing layout shift and blocking UI elements
### Environment: Production (Vercel)
Frontend: https://acp-front-nu.vercel.app
API: https://acp-api-w2ng.onrender.com
Browser: Chrome 146.0.7680.165
Date: 05.04.2026
### Preconditions:
User opens the homepage
Application loads successfully
API requests are completed without errors
### Steps to Reproduce:
Open the main page
Wait until the page fully loads
Start scrolling down the page
Observe the behavior of the header and underlying content
### Actual Result:
Header overlaps the main content while scrolling
UI elements (e.g., forms, inputs, buttons) shift or become partially hidden
Some interactive elements may become inaccessible due to overlay.
### Expected Result:
Header should remain properly positioned (fixed or sticky without overlap issues)
Page content should not shift or be covered
All UI elements should remain fully visible and accessible during scroll
### Priority: Medium
### Severity: Medium
### Additional findings:
### Issue is inconsistent depending on field state:
- Inactive fields (route, time) are overlapped by footer
- Active fields (date, passengers) are displayed correctly above footer
### Reproducible on:
- Desktop small (1366x768)
- iPad Air (820x1180)

## BUG-004: Profile data is not loaded after page refresh due to failed API request
### Title:
Profile data is not loaded after page refresh (Failed to fetch error)
### Environment:
Production (Vercel)
https://acp-front-nu.vercel.app
Browser: Chrome 146.0.7680.165
Device: Desktop / Mobile (DevTools)
### Description:
Profile data fails to load after page refresh.
The UI shows "Failed to fetch" error and profile fields are empty.
The issue is intermittent:
- Sometimes profile loads correctly
- Sometimes API request fails after refresh
### Steps to Reproduce:
1. Login to the application
2. Navigate to Profile page
3. Refresh the page (F5)
4. Observe profile loading
### Actual Result:
"Failed to fetch" error is displayed
Profile data is not loaded
Network request to /users/profile fails or is blocked
### Expected Result:
Profile data should load correctly after page refresh.
### Priority: High
### Severity: High
### Additional info:
API works correctly via Postman (returns 200 OK with valid token)
Issue may be related to token handling or authorization on frontend


## BUG-005: Language switch(UA/EN) is not displayed on iPad
### Title:
Bug – Language switch icons are missing on iPad
### Environment:
- Production (Vercel)
- URL: https://acp-front-nu.vercel.app
- Device: iPad (768x1024)
- Browser: Chrome DevTools (mobile emulation)
- OS: iOS (emulated)
- Zoom: 100%
- Date: 07.04.2026
### Preconditions:
- User opens the homepage
- Page loads successfully
### Steps to Reproduce:
1. Open the homepage
2. Enable device toolbar (Ctrl + Shift + M)
3. Select iPad (768x1024)
4. Observe the header
### Actual Result:
- Language switch icons (UA / EN) are not displayed in the header
### Expected Result:
- Language switch icons (UA / EN) are visible and accessible in the header
### Priority: Medium
### Severity: Medium (UI / functionality)
### Notes:
- Language icons are visible on mobile and/or desktop resolutions
- Issue occurs only on iPad resolution

## BUG-006: Login form is misaligned on iPad(layout broken)
### Title:
Bug – Login form is misaligned on iPad (not centered)
### Environment:
- Production (Vercel)
- URL: https://acp-front-nu.vercel.app/login
- Device: iPad (768x1024)
- Browser: Chrome DevTools (mobile emulation)
- Zoom: 100%
- Date: 07.04.2026
### Preconditions:
- User opens the login page
### Steps to Reproduce:
1. Open the login page
2. Enable device toolbar (Ctrl + Shift + M)
3. Select iPad (768x1024)
4. Observe the login form layout
### Actual Result:
- Login form is not centered
- Form is aligned to the left side of the screen
- Layout looks broken and unbalanced
- Excess empty space on the right side
### Expected Result:
- Login form should be centered on the screen
- Layout should be properly aligned and visually balanced
- UI should adapt correctly for tablet resolution
### Priority: High
### Severity: Medium (UI / UX issue)
### Notes:
- Layout looks correct on mobile devices
- Issue appears only on tablet resolution (iPad)
- Likely related to incorrect responsive layout handling

## BUG-007: Footer layout issues on Desktop
### Title:
Bug – Footer layout issues on Desktop (1366x768): text clipping and insufficient spacing with page content
### Environment:
- Production (Vercel)
- URL: https://acp-front-nu.vercel.app
- Device: Desktop Small (1366x768)
- Browser: Chrome DevTools (mobile emulation)
- Zoom: 100%
- Date: 07.04.2026
### Preconditions:
- User opens the homepage
- Page loads successfully
### Steps to Reproduce:
1. Open the homepage
2. Scroll down to the bottom of the page
3. Observe the footer section
4. Check the copyright text and spacing between content (map) and footer
### Actual Result:
- Footer text is partially cut off at the bottom (e.g., last characters of the year are not fully visible)
- Insufficient spacing between page content and footer
- Map content (Google Maps labels) appears too close to the footer, causing visual crowding
### Expected Result:
- Footer text should be fully visible without clipping
- Proper spacing (padding/margin) should be maintained between content and footer
- Layout should be visually balanced and readable
### Priority: Low
### Severity: Low (UI issue)
### Notes:
- Issue reproducible on Desktop Small resolution (1366x768)
- Likely related to CSS (container height, overflow, or missing spacing)
- Multiple manifestations indicate a layout consistency issue in the footer section

## BUG-008: Infinite repeated requests to /api/v1/trips endpoint on page load
### Environment:
Production: ﻿VercelPassenger transportation and ticket booking | Autolux Cherkasy-Plus﻿
Browser: Chrome 146.0.7680.165
### Preconditions:
User opens the main page
### Steps to reproduce:
Open the website
Open DevTools (F12)
Navigate to the Network tab
Filter requests by trips
### Actual result:
Continuous requests are sent to /api/v1/trips without any user interaction
Number of requests rapidly increases (hundreds within seconds)
Status codes: 200 OK and 304 Not Modified
Requests continue indefinitely
### Expected result:
A single request (or limited number of requests) should be sent on page load
No repeated requests without user interaction unless intentional polling is implemented
###Additional information:
Issue occurs immediately after page load
Requests are triggered even when response data does not change
May indicate infinite re-render or incorrect dependency handling in frontend (e.g. useEffect)
Can lead to performance degradation and unnecessary server load
 **User impact:**
User cannot select route or time, booking flow is blocked
 **UI note:**
Form remains in loading state ("Завантажуємо рейси..."), fields are disabled
 Retest result: 
The issue is no longer reproducible.
- No infinite API requests observed after page reload
- Requests to /api/v1/trips are stable (1–2 requests) and do not repeat continuously
- No increase in request count over time (no loop)
- Trips list loads correctly
- Route and time selection work as expected
- UI remains stable (no layout shift during loading)
Console:
- No critical errors observed
- Only non-blocking preload warnings present
Fix verified.


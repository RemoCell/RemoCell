# RemoCell

Remote cell phone (mobile) coverage data. Not the cell tower locations, but actual signal strength.

Offline-friendly.

Crowd-sourced. Always free.


## PERMANENT SCOPE

Mainstream only. Limited to:

- remote areas - excluding areas with evenly spread good enough signal coverage
- "remote-friendly" carriers
  - no city/metropolitan-only carriers (like Freedom Mobile in Canada)
  - data-only carriers are OK if they are not exclusive to cities/metropolitan areas. For example,
    TextNow (virtual US data-only carrier).
- ground-level (or ground-accessible public structures/buildings, like dams, bridges, watch
  towers...) - no flights/baloons/cable cars
- signal
  - no categorizing by roads/paths or car/biking/walking/hiking speed or handicap/accessibility
  - no collection of other data (road conditions, hiking trails...)
  - signal strength - no bandwidth (speed)/latency testing
  - data - no interpretation (awful, weak, good...), because for the same signal strength reception
    varies by device.
- Android (for uploading) - iPhone/iPbut they would be too big. ad makes accessing signal strength
  difficult
- app download over a fairly good connection
- not optimized for manual download of data:
  - Big files - we use partial download only for areas you need.
  - Potentially many files (or parts of) to download (for a chosen area).
  - Downloaded data needs to be collated/merged/re-indexed...
- Not optimized to be updated frequently. Towers don't grow overnight. Optimizing data storage for
  frequent updates would involve much more GitHub processing and complexity.
- Optimized to be free (storage on GitHub - any other mainstream is too limited, or costly) and
  usable offline in the app.
- Storage is on GitHub: free, big data, ongoing processing. But, our data can always be replicated
  elsewhere.
- No web "API". This is for end users.
- No support for 3rd parties by default. Storage is primarily in binary form. The formats,
  filesystem and reference notations/patterns and scheduling of updates may change without notice.
- Simple privacy (fuzzying submission delay, excluding chosen areas).
- Latitude/longitude coordinates, "standard" GPS accuracy.
- Cell phone (mobile) or tablets only - no easy website.

## LONGTERM SCOPE

- English (user interface)
- Google Maps (on Android, maybe on iPhone/iPad) for reading/using
- No cellular tower data (like opencellid.org) - it doesn't help because of terrain.
- No data verification/vetting.
- No server-side filtering of "civilized" or "no coverage at all". Filtered in the uploading app only.
- No sharing/attributing data between "primary" and "virtual" carriers/networks. The user can pick
  several carriers to show. That isolates problems when a virtual carrier may migrate to another
  primary later.

## MIDTERM SCOPE

- No iPhone/iPad app (not even to read). Subscribe to a tracking issue.
- No fancy or one/integrated cell app. Repeatitive manual steps, switching between apps.
- Needing [NetMonitor Cell Signal Logging = Net Monitor
  Lite](https://play.google.com/store/apps/details?id=ru.v_a_v.netmonitor) Android app for
  uploading.
- No data pruning.

## NON-PUBLIC INITIAL SCOPE

- No privacy filters. Subscribe to a tracking issue.
- Updates by full download (of the chosen areas) only.

## ROADMAP

- back-end, test units
- basic functionality
- "telemetrics"/statistics: figuring out most popular map dimensions, retention and update frequency, so that we choose storage parameters
- temporary only: multiple slice widths to compare user experience
- test back-end
- privacy: fuzzing submission delay
- privacy: optional direct source (to avoid fuzzying and its delay)
- privacy: exclude "Home/Accommodation/Work..." area(s)
- per instance/installation upload sets - rather than per GitHub user: so that a group of people
  can use the same GitHub account
- Apple (iOS) read-only app


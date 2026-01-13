Art Institute of Chicago – Artwork DataTable (React)
Overview

This project is a React application built using Vite and TypeScript that displays artwork data from the Art Institute of Chicago API using a PrimeReact DataTable.

The application demonstrates:

Server-side pagination

Persistent row selection across paginated data

Custom row selection without prefetching

Strict adherence to memory and performance constraints

This project was implemented as part of a React internship assignment and follows all provided technical and architectural requirements.

Live Demo

(Add deployed URL here after deployment)

Tech Stack

Frontend: React 18

Build Tool: Vite

Language: TypeScript (strict mode)

UI Library: PrimeReact

API: Art Institute of Chicago Public API

API Used
https://api.artic.edu/api/v1/artworks?page=1


Data is fetched one page at a time

No bulk data fetching

No prefetching of future pages

Features Implemented
1. Server-Side Pagination

Pagination is handled entirely by the server

Only the currently requested page is fetched

Page navigation triggers a new API request

Previously visited pages are not cached

This approach ensures scalability and avoids unnecessary memory usage.

2. DataTable with Required Fields

The following fields are displayed as required:

title

place_of_origin

artist_display

inscriptions

date_start

date_end

3. Row Selection

Individual rows can be selected or deselected using checkboxes

Selection logic is independent of pagination

Selection state is not tied to the table’s data source

4. Persistent Selection Across Pages

Selected rows remain selected when navigating between pages

No row objects are stored in memory

Only unique row identifiers are tracked

Selection Strategy
useRef<Set<number>>

One set tracks selected row IDs

Another set tracks explicitly deselected row IDs

This approach allows selection persistence without violating server-side pagination constraints.

5. Select All / Deselect All (Current Page Only)

Users can select or deselect all rows on the currently visible page

Other pages remain unaffected

No assumptions are made about data on other pages

6. Custom Row Selection (Critical Requirement)

Users can input a number N

The application selects only the first N rows of the current page

If N exceeds the number of available rows, all rows on the current page are selected

Existing selections on the current page are reset deterministically

No API calls are made during this operation.
No loops over pages are used.
No data from other pages is fetched or stored.

7. UI Hardening and Error Handling

Loading indicator displayed during API requests

Graceful error handling for failed network requests

Selection controls disabled when no data is available

Live selection count display (e.g., “Selected: 8 rows”)

Server-side pagination report:

Showing 1 to 12 of 130023 entries

Explicitly Avoided (Per Assignment Rules)

Prefetching multiple pages

Fetching all data at once

Storing row objects from other pages

Loop-based API calls in custom selection

Client-side pagination

Testing Checklist

Navigate between pages and verify selection persistence

Use custom selection with large values and confirm no prefetching

Verify network tab shows:

One API call per page change

Zero API calls during selection operations

Confirm memory usage remains stable

How to Run Locally
npm install
npm run dev


The application runs on:

http://localhost:5173

Project Structure (Simplified)
src/
 ├─ api/
 │   └─ artworksApi.ts
 ├─ types/
 │   └─ artwork.ts
 ├─ App.tsx
 └─ main.tsx

Key Design Decision

Selection state is stored as intent (row IDs) rather than data (row objects), allowing persistence across pages without violating server-side pagination constraints.

Assignment Compliance Summary
Requirement	Status
Vite + TypeScript	Implemented
PrimeReact DataTable	Implemented
Server-side pagination	Implemented
Persistent selection	Implemented
Custom selection without prefetching	Implemented
Memory-safe architecture	Implemented
Author

Sharvari Bhagat

License

This project is intended for evaluation purposes only.
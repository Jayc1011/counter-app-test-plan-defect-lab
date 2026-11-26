# Lab: Test Planning and Defect Management — Counter Application

## Step 1: Test Plan

### Test Objectives
- Verify that the Counter application initializes to Count: 0 and updates the displayed count accurately for valid interactions.
- Confirm that the Increment, Decrement, and Reset controls behave reliably across single and sequential actions.
- Identify functional defects, boundary/edge-case issues, or unexpected state changes and document reproducible findings.

### Scope
- In Scope:
  - Initial rendered state on load (Count: 0 and visible action buttons).
  - Increment, Decrement, and Reset button actions and multi-step sequences.
  - Browser UI state updates and visual rendering.
- Out of Scope:
  - Backend APIs, databases, and authentication (client-side only application).
  - Load/performance testing, security testing, and mobile device layout testing.
  - React, Vite, or TypeScript framework internals.

### Testing Approach
- Manual Functional and Sequence Testing: Run structured test cases in the browser against the local Vite server (npm run dev) and compare actual UI behavior against expected results.
- Boundary and Edge-Case Testing: Check starting state (0), repeated clicks, and state transitions after multi-step sequences.
- Build and Lint Verification: Run npm run lint and npm run build to verify there are no lint or TypeScript errors.
- Confirmation Testing: Re-run any failed test case multiple times to confirm reproducibility before logging a defect report.

### Test Environment and Tools
- Application: counter-app (React 19.2.8, TypeScript 6.0.2, Vite 8.3.0)
- OS / Runtime: Windows with WSL, Node.js, npm
- Browser: Desktop browser (Chrome / Edge)
- Tools: VS Code, terminal, browser DevTools, Git and GitHub

### Product Risks
- Incorrect state updates or wrong arithmetic in button handlers (for example, adding instead of subtracting on Decrement or failing to reset to 0) can show wrong counts.
- Rapid or multi-step interactions can expose state or UI inconsistencies.

### Entry and Exit Criteria
- Entry Criteria:
  - Dependencies are installed (npm install succeeds).
  - Application runs locally via npm run dev without runtime errors.
  - Test plan and at least four test cases are written.
- Exit Criteria:
  - All planned test cases are executed with actual results, Pass/Fail status, and reproducibility notes for failures.
  - At least one reproducible defect report is completed (or a statement that no defects were found with executed tests listed).
  - Changes are committed and pushed to a public GitHub repository.

## Step 2: Design Test Cases

### TC-001: Verify Initial Counter State on Page Load
- **Test Case ID:** TC-001
- **Starting State:** Application is loaded fresh in the browser (http://localhost:5173) with no prior button clicks.
- **Actions:**
  1. Open the Counter application in the browser.
  2. Observe the displayed count heading and action buttons (Increment, Decrement, Reset).
- **Expected Result:** Heading displays "Count: 0", and Increment, Decrement, and Reset buttons are visible and enabled.

### TC-002: Verify Increment Button Increases Count by 1
- **Test Case ID:** TC-002
- **Starting State:** Application is loaded on the main page with "Count: 0".
- **Actions:**
  1. Click the Increment button once.
- **Expected Result:** Displayed count increases by 1 from 0 to 1 ("Count: 1").

### TC-003: Verify Decrement Button Decreases Count by 1
- **Test Case ID:** TC-003
- **Starting State:** Application is loaded on the main page with "Count: 2" (after clicking Increment twice).
- **Actions:**
  1. Click Increment twice so the display shows "Count: 2".
  2. Click Decrement once.
- **Expected Result:** Displayed count decreases by 1 from 2 to 1 ("Count: 1").

### TC-004: Verify Multi-Step Sequence and Reset Functionality
- **Test Case ID:** TC-004
- **Starting State:** Application is loaded on the main page with "Count: 0".
- **Actions:**
  1. Click Increment three times.
  2. Click Decrement once.
  3. Click Reset once.
- **Expected Result:** After step 1, display shows "Count: 3". After step 2, display shows "Count: 2". After step 3, display resets to "Count: 0".

## Step 3: Execute the Tests

| Test Case ID | Actual Result | Pass / Fail | Reproducibility Check |
| ------------ | ------------- | ----------- | --------------------- |
| TC-001 | Page loaded and displayed "Count: 0" with Increment, Decrement, and Reset buttons. | Pass | N/A |
| TC-002 | Clicking Increment once changed display from "Count: 0" to "Count: 1". | Pass | N/A |
| TC-003 | Starting from "Count: 2", clicking Decrement once changed display to "Count: 3" instead of "Count: 1". | Fail | Repeated twice after page refresh; reproduced consistently every time ("Count: 2" -> "Count: 3"). |
| TC-004 | Three Increment clicks showed "Count: 3", one Decrement click changed display to "Count: 4" instead of "Count: 2", and Reset returned display to "Count: 0". | Fail | Repeated twice from a fresh reload; Decrement consistently added 1 during the sequence while Reset returned "Count: 0". |

## Step 4: Report a Defect

### DEF-001: Decrement button increments count by 1 instead of decrementing by 1
- **Defect ID and Title:** DEF-001 — Decrement button increments count by 1 instead of decrementing by 1
- **Related Test Case:** TC-003 (also affects TC-004)
- **Test Environment:** counter-app (React 19.2.8, TypeScript 6.0.2, Vite 8.3.0), Windows with WSL, Node.js/npm, desktop browser
- **Steps to Reproduce:**
  1. Run the app locally with npm run dev and open http://localhost:5173 in a browser.
  2. Click Increment twice so the display shows "Count: 2".
  3. Click Decrement once.
- **Expected Result:** Count decreases by 1 to "Count: 1".
- **Actual Result:** Count increases by 1 to "Count: 3".
- **Severity and Priority:** High severity, P1 priority
- **Status:** Open (in `src/App.tsx`, Decrement calls `setCount(count + 1)` instead of `setCount(count - 1)`)

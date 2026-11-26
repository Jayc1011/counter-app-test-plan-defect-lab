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

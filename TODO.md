# TODO: Aligning Code with Specification

This document outlines the discrepancies found between the current implementation in `Code.gs` and the technical requirements detailed in `SPEC.md`.

**Note on Scope:** The `SPEC.md` focuses primarily on the `=GEMINI()` custom function. The `README.md` and `Code.gs` include additional features like the "Gemini AI" menu for processing selected cells, which are not covered by the spec. The following points are focused on aligning the core `=GEMINI()` function with its specification.

---

### 1. Implement Graceful Error Handling in `=GEMINI()`

**Issue:** The `GEMINI` custom function does not handle API errors gracefully. It allows exceptions from the `callGeminiAPI` helper function to bubble up, which results in a generic `#ERROR!` in the Google Sheet cell. The user must hover over the cell to see the error message.

**Requirement:** The spec (Section 6) requires that descriptive error messages be *returned* as a string directly into the cell.

**Task:**
-   In `Code.gs`, wrap the `callGeminiAPI(...)` call inside the `GEMINI` function within a `try...catch` block.
-   The `catch` block should return the error message from the caught exception, ensuring it is displayed in the cell.

### 2. Standardize Error Message Formatting

**Issue:** Many of the error messages returned or thrown by the script do not match the exact format specified in `SPEC.md`.

**Requirement:** The error messages should be consistent and follow the format outlined in `SPEC.md` (Section 6) to provide clear, actionable feedback to the user.

**Tasks:**

#### a. API Call Failures (Client & Server Errors)
-   **Spec:**
    -   `ERROR: API call failed (Code 400): [Detailed message from API]`
    -   `ERROR: API call failed with server error (Code 500).`
-   **Current:** `API call failed with response code ${responseCode}. Message: ${errorResponse.error.message}`
-   **Action:** In `callGeminiAPI`, differentiate between 4xx and 5xx HTTP status codes to provide the specific error message format for client vs. server errors.

#### b. Safety Block Responses
-   **Spec:** `ERROR: Response blocked for safety reasons. [Finish Reason]`
-   **Current:** `API call finished with reason: ${candidate.finishReason}`
-   **Action:** In `callGeminiAPI`, when a response is blocked, format the returned string to match the spec, including the `ERROR:` prefix and the "Response blocked for safety reasons" text.

#### c. Network/Fetch Failures
-   **Spec (Implied):** `ERROR: Failed to call the Gemini API: [Exception message]` (to be returned by `=GEMINI()`).
-   **Current:** The error is thrown from `callGeminiAPI` and not handled by `GEMINI`.
-   **Action:** Ensure the `try...catch` block in the `GEMINI` function (from Task 1) formats the caught exception message to match the spec's format, including the `ERROR:` prefix.

#### d. Invalid Input Prompts
-   **Spec:** `ERROR: Prompt cannot be empty.`
-   **Current:** `Error: Prompt cannot be empty.` and `Error: Prompt text is empty after combining cells.`
-   **Action:** In the `GEMINI` function, standardize the case to `ERROR:` for all user-input validation messages to align with the rest of the spec's error formats.

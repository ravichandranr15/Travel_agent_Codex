# AI-Assisted Trip Details Specification

## Purpose

Let a traveler describe a trip in ordinary language and identify the details needed to create it: destination, travel dates, and trip type. This is the fifth product specification. The conversational UI and its visual behavior belong in `frontend-spec.md`; this document defines AI behavior and the data passed to the existing trip-creation flow.

## Scope and Constraints

- Accept free-form user input and extract the required trip details.
- Do not add or change backend endpoints, persistence, or server-side business logic.
- Reuse the application's existing trip types, date rules, and trip-creation flow. Do not invent new trip categories or change how trips are stored.
- Do not assume a particular AI provider or model. The implementation must use an already approved client-side capability. Never expose a private provider key in frontend code. If no safe client-side capability is available, resolve that dependency before implementation; adding a backend is outside this spec.

## Required Output

For each conversation, produce structured values equivalent to:

```json
{
  "destination": "string or null",
  "startDate": "YYYY-MM-DD or null",
  "endDate": "YYYY-MM-DD or null",
  "tripType": "existing application value or null",
  "missingFields": ["destination", "startDate", "endDate", "tripType"],
  "needsConfirmation": true
}
```

Only include values supported by the user's message or confirmed follow-up. Null means unknown; do not guess a destination, dates, or trip type. Preserve the application's canonical trip-type values in the result.

## Conversation Behavior

1. Extract any clear values from the initial free-form description, including values expressed in different orders or together (for example, “A week in Tokyo in April for food and museums”).
2. Ask concise follow-up questions only for required fields that are missing or ambiguous. Ask one focused question at a time and retain already understood values.
3. Resolve relative dates only when the current date is available to the AI flow. Convert dates to the application's required format; if a year, range, or interpretation is unclear, ask rather than assume. Do not silently reinterpret invalid or past dates.
4. Before trip creation, present the extracted destination, date range, and trip type for user confirmation. Allow the user to correct any value. Trigger the existing create-trip flow only after confirmation and when all required values pass existing validation.
5. If the AI capability is unavailable, returns unusable data, or cannot understand an answer, keep the conversation recoverable and let the user retry or enter the details through the existing trip flow. Do not create a partial trip.

## Integration and Privacy

Keep the AI result separate from persistence: the existing frontend flow remains responsible for validation and trip creation. Send only the user's current trip-planning conversation to the AI capability; do not include account credentials or unrelated trip data. Do not log conversation text or provider secrets.

## Acceptance Criteria

- A user can provide all required details in one free-form message and review the extracted values.
- Missing or ambiguous required details prompt for clarification without losing known values.
- The user can correct extracted values before creation; no trip is created without explicit confirmation.
- AI errors and unavailable capability do not block access to the existing manual trip-entry path.
- No backend change or exposed private AI credential is required by the implementation.

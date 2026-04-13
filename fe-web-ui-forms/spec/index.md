# Frontend Web UI and Forms — Non-Negotiable Rules

## Scope
This file owns input flows, validation presentation, submission lifecycle, destructive actions, and UI state completeness.

## Violations
- form submits without disabled/pending protection and can duplicate user action — ERROR
- validation shown only after failed submit when inline early feedback is required — ERROR
- loading state hides context and causes layout jump — ERROR
- destructive action has no confirmation or undo strategy where risk is material — ERROR
- field error not associated with the field and recovery path — ERROR
- submit action enabled when required data is clearly invalid — ERROR

## UI States
- MUST define loading, empty, error, success, and partial-data states for user-visible surfaces.
- MUST keep layout stable during loading where practical.
- MUST avoid dead-end states with no recovery path.

## Forms
- MUST define validation ownership: client, server, or both.
- MUST validate before submission when the rule is available on the client.
- MUST surface server validation back to fields or form summary as appropriate.
- MUST preserve user input on recoverable failures.
- MUST prevent accidental duplicate submission.
- MUST expose pending state on submit actions.
- MUST support keyboard submission where semantically appropriate.

## Validation UX
- MUST make required fields, constraints, and irreversible effects clear before submit.
- MUST show field-level errors near the relevant control.
- MUST show form-level errors for cross-field or server failures.
- MUST clear resolved errors when inputs become valid.

## Destructive and Irreversible Actions
- MUST require confirmation, undo, or an equivalent safety mechanism when user harm is material.
- MUST make destructive actions visually distinct.
- MUST not default focus to destructive confirmation when safer alternatives exist.

## Formatting and Masking
- MUST separate display formatting from submitted value.
- MUST normalize user input before validation when normalization is safe and expected.
- MUST not use input masks that trap cursor movement or block valid paste behavior.

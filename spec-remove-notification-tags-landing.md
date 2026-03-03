# Spec: Remove Notification Obligation Tags from Landing Page

## Summary

Remove the notification obligation sub-labels from both choice buttons on the landing page. The landing screen should present only the choice between "New arrangement" and "Reassessment" — not pre-load regulatory conclusions before the user has answered any questions.

## Motivation

**UX simplification.** The `landing-choice-tag` spans surface notification obligation statements before the user has provided any input. This is premature: notification obligations are outputs of the classification process, not inputs to it. Displaying them on the landing screen creates cognitive overhead and may mislead users who have not yet completed the decision tree.

Notification obligation information remains fully available on result pages where it is contextually appropriate.

## Scope

### In scope
- Remove the `<span class="landing-choice-tag">` element from the "New arrangement" button
- Remove the `<span class="landing-choice-tag">` element from the "Reassessment" button
- Remove the `.landing-choice-tag` CSS style block (no remaining consumers after the HTML change)

### Out of scope
- Result pages — BaFin notification sections (`bafin` property on each result) are untouched
- All decision-tree question nodes — no changes
- Application logic, routing, state management — no changes

## Affected Files

| File | Change |
|------|--------|
| `index.html` | Remove two `<span class="landing-choice-tag">` elements in `renderLanding()` |
| `index.html` | Remove `.landing-choice-tag` CSS rule block |

## Detailed Changes

### 1. HTML — `renderLanding()` function

**Remove** from the "New arrangement" button:
```html
<span class="landing-choice-tag">Notification obligations under § 25b KWG, MaRisk AT 9, and DORA Art. 28(2) are subject to assessment</span>
```

**Remove** from the "Reassessment" button:
```html
<span class="landing-choice-tag">Notification obligations under § 25b KWG and MaRisk AT 9 arise only upon change in materiality classification</span>
```

### 2. CSS — `.landing-choice-tag` style block

**Remove** the entire `.landing-choice-tag` rule (exact lines to be confirmed at implementation time). The class will have no remaining usages in the file.

## Acceptance Criteria

- [ ] Landing page renders both choice buttons without any notification obligation sub-label
- [ ] No orphaned `.landing-choice-tag` CSS rule remains in the file
- [ ] All result pages continue to display BaFin notification sections unchanged
- [ ] No visual regressions on the landing page (button layout, sizing, spacing remain intact after tag removal)
- [ ] No JavaScript errors introduced

## Risk Assessment

**Low risk.** This is a purely cosmetic HTML/CSS removal. No application logic, data flow, routing, or result content is affected. The change is confined to the `renderLanding()` function and one CSS rule block.

# Accessibility & Semantic HTML Audit (WCAG 2.2)

This report details the findings of an accessibility and semantic HTML audit conducted on the project's HTML templates. Issues are categorized based on WCAG 2.2 guidelines, followed by a prioritized plan for remediation.

## Detailed Analysis

### 1. Semantic HTML & ARIA Usage

**Issue: Improper Stepper Semantics**
- **Context:** The main progress stepper component is built with `div` elements. It functions as the primary navigation through the application's multi-step process but is not marked up as a navigation landmark.
- **Risks:** Screen reader users cannot identify this as a navigation block or easily determine the current step. This fails WCAG 1.3.1 (Info and Relationships) and WCAG 4.1.2 (Name, Role, Value).
- **Example:** `app/shared/components/stepper.html`

**Issue: Non-Semantic Lists and Interactive Elements**
- **Context:**
  - In the Checklist feature, preparation items are `div`s instead of `<li>` elements within a `<ul>`.
  - In the Sounds feature, the clickable sound options are `div`s with `(click)` handlers, not `<button>` elements.
- **Risks:** Elements that are visually lists or buttons do not have the correct semantic role. This prevents assistive technologies from interpreting them correctly and removes expected keyboard functionality (e.g., spacebar activation for buttons). This fails WCAG 4.1.2 (Name, Role, Value).
- **Examples:** `app/features/checklist/checklist.html`, `app/features/sounds/sounds.html`

**Issue: Missing Accessible Names for Form Inputs**
- **Context:** In the Checklist, the `input[type="checkbox"]` is not programmatically linked to its visible text description. The `textarea` in the Reflection component is also not linked to its visible heading.
- **Risks:** Screen reader users won't know what the checkbox or textarea is for, as the label is not associated with the control. This fails WCAG 1.3.1 and WCAG 4.1.2.
- **Examples:** `app/features/checklist/checklist.html`, `app/features/reflection/reflection.html`

**Issue: Missing ARIA Attributes for State**
- **Context:**
  - The active step in `stepper.html` is indicated by color only.
  - The selected sound in `sounds.html` is indicated by a visual ring only.
  - The progress bar in `checklist.html` is a simple `div` and lacks ARIA roles.
- **Risks:** State information (e.g., "this is the current step," "this button is pressed," "progress is 50%") is not available to screen reader users. This fails WCAG 1.3.1.
- **Examples:** `app/shared/components/stepper.html`, `app/features/sounds/sounds.html`, `app/features/checklist/checklist.html`

### 2. Keyboard Navigation & Focus Order

**Issue: Inaccessible Custom Rating Component**
- **Context:** The star rating in the Reflection feature is made of `<i>` icon tags with `(click)` handlers.
- **Risks:** This component is completely inoperable via keyboard. A user cannot navigate to or select a rating using Tab or arrow keys. This is a critical failure of WCAG 2.1.1 (Keyboard).
- **Example:** `app/features/reflection/reflection.html`

**Issue: Use of Non-Interactive Elements for Click Actions**
- **Context:** The sound selection items are `div`s, which are not focusable by default and do not have button semantics.
- **Risks:** Keyboard users cannot tab to these elements to select a sound. This fails WCAG 2.1.1 (Keyboard).
- **Example:** `app/features/sounds/sounds.html`

### 3. Screen Reader Compatibility

**Issue: Dynamic Content Changes Are Not Announced**
- **Context:** In the Breathing and Timer components, critical information like the breathing instruction ("Inhale," "Exhale"), countdowns, and the running timer are updated visually but not announced by screen readers.
- **Risks:** A screen reader user is unaware of the application's state changes, making these core features unusable. This fails WCAG 4.1.3 (Status Messages).
- **Examples:** `app/features/breathing/breathing.html`, `app/features/timer/timer.html`

**Issue: Ambiguous Link/Button Content**
- **Context:** Many buttons contain only an icon (e.g., the delete and add buttons in the Checklist). While some have text, the icons themselves are not hidden from screen readers.
- **Risks:** Screen readers may announce the icon's class names (e.g., "fas fa-trash-alt"), which is unhelpful. Buttons with only icons lack an accessible name. This violates WCAG 4.1.2.
- **Examples:** `app/features/checklist/checklist.html`, `app/shared/components/navigation.html`

### 4. Color Contrast & Visual Cues

**Issue: Insufficient Text Contrast on Disabled Buttons**
- **Context:** The "Continue" button in the navigation component, when disabled, uses `text-slate-400` on a `slate-600/700` gradient background.
- **Risks:** The text-to-background contrast ratio is approximately 2.87:1, which fails the WCAG 2.2 minimum requirement of 4.5:1 for normal text. Users with low vision may not be able to read the button text.
- **Example:** `app/shared/components/navigation.html`

---

## Accessibility & Semantics Improvement Plan

### High Priority
- [ ] **(Reflection)** Re-implement the star rating as a keyboard-accessible control, such as a series of styled radio buttons or a custom element with `role="slider"`.
- [ ] **(Sounds)** Convert the clickable `div` elements for sound selection into `<button>` elements to make them focusable and announce their role correctly.
- [ ] **(Checklist)** Associate each `input[type="checkbox"]` with its text by using a `<label>` element with a `for` attribute.
- [ ] **(Stepper)** Add `aria-current="step"` to the active step's element to programmatically indicate its status.
- [ ] **(Breathing & Timer)** Use an `aria-live` region to announce dynamic text changes (e.g., instructions, countdowns, timer status) to screen reader users.
- [ ] **(Navigation)** Adjust the color of disabled button text (`text-slate-400`) to meet the 4.5:1 contrast ratio against its background.
- [ ] **(Checklist)** Provide an `aria-label` for the icon-only delete button to describe its function (e.g., `aria-label="Delete item: {{item.text}}"`).

### Medium Priority
- [ ] **(Stepper)** Change the root element of the stepper to `<nav>` and the steps to an ordered list (`<ol>` with `<li>`) to reflect its navigational purpose.
- [ ] **(Checklist)** Convert the `div`-based list of tasks into a semantic `<ul>`.
- [ ] **(Checklist)** Implement the progress bar using `role="progressbar"` and the required `aria-valuenow`, `aria-valuemin`, and `aria-valuemax` attributes.
- [ ] **(Sounds)** Use `aria-pressed="true/false"` on the sound selection buttons to indicate which sound is currently active.
- [ ] **(Reflection)** Programmatically link the "Notes & Distractions" heading to the `textarea` using `aria-labelledby`.
- [ ] **(Global)** Add `aria-hidden="true"` to all decorative icons (`<i>` tags) to prevent them from being announced by screen readers.

### Low Priority
- [ ] **(Welcome)** For the SVG logo, add a `<title>` element for accessibility or ensure it has `role="img"` and is marked as decorative if appropriate.

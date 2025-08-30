# Tailwind CSS v4 Adoption Audit Report

This report provides a comprehensive audit of the project for Tailwind CSS v4 adoption and best practices. The codebase is already in excellent shape and demonstrates a strong understanding of modern Tailwind principles. The following points are primarily recommendations for even tighter alignment with the v4 CSS-first philosophy.

## Detailed Analysis

### CSS-First Configuration (`@theme`)

*   **Context**: `src/styles.css`
*   **Issue**: Theme customizations are defined using CSS custom properties (`--color-amber-500: #f59e0b;`).
*   **Impact**: While this is valid CSS, it's not the most idiomatic way to define theme values in Tailwind v4. The `@theme` directive is designed to directly configure Tailwind's design tokens.
*   **V4 Recommendation**: Define theme values directly within the `@theme` block. This makes the values directly available to Tailwind's utility classes and as CSS variables.

    ```css
    /* src/styles.css */
    @theme {
      colors: {
        amber-500: #f59e0b;
        orange-600: #ea580c;
        slate-900: #0f172a;
        /* ...and so on */
      }
    }
    ```

### CSS Entry Point

The project correctly uses `@import "tailwindcss";` in `src/styles.css` and contains no deprecated `@tailwind` directives. **No issues found.**

### Utility & Variant Syntax

*   **Context**: `src/app/features/breathing/breathing.html` and other component templates.
*   **Issue**: The code uses separate width and height utilities (e.g., `w-48 h-48`).
*   **Impact**: This is not an error, but it misses an opportunity to use the new, more concise `size-*` utilities available in Tailwind v4.
*   **V4 Recommendation**: Replace separate width and height utilities with the `size-*` utility where applicable.

    ```html
    <!-- Before -->
    <div class="relative w-48 h-48 mx-auto mb-8">...</div>

    <!-- After -->
    <div class="relative size-48 mx-auto mb-8">...</div>
    ```

### Performance & Maintainability

*   **Context**: `src/styles.css`
*   **Issue**: Overuse of `@apply` for base styles, particularly for form elements.
*   **Impact**: While functional, this approach is a holdover from older Tailwind versions. V4's CSS-first approach encourages using native CSS with theme variables for base styling, which can be more performant and easier to maintain.
*   **V4 Recommendation**: Refactor `@apply` rules to use native CSS properties and Tailwind's theme variables.

    ```css
    /* Before */
    @layer base {
      input[type='checkbox'] {
        @apply rounded bg-slate-900 border-slate-700 text-amber-500 focus:ring-amber-500 focus:ring-offset-slate-800;
      }
    }

    /* After */
    @layer base {
      input[type='checkbox'] {
        border-radius: theme(borderRadius.md);
        background-color: theme(colors.slate-900);
        border-color: theme(colors.slate-700);
        color: theme(colors.amber-500);
      }
      input[type='checkbox']:focus {
        --tw-ring-color: theme(colors.amber-500);
        --tw-ring-offset-color: theme(colors.slate-800);
      }
    }
    ```

*   **Context**: `src/styles.css`
*   **Issue**: A custom `.sr-only` utility class is defined.
*   **Impact**: This is redundant, as Tailwind CSS includes a built-in `sr-only` class that provides the same functionality. Maintaining a custom version can lead to inconsistencies.
*   **V4 Recommendation**: Remove the custom `.sr-only` class and use Tailwind's built-in `sr-only` utility instead.

## Tailwind v4 Improvement Plan

### High Priority
- [ ] Migrate all theme customizations from CSS custom properties to the `@theme` block in `src/styles.css`.
- [ ] Remove the custom `.sr-only` utility from `src/styles.css` and use the built-in `sr-only` class where needed.

### Medium Priority
- [ ] Refactor `@apply` rules in `src/styles.css` to use native CSS properties and `theme()` variables for better alignment with v4's CSS-first philosophy.
- [ ] Audit the HTML templates and replace separate width/height utilities (e.g., `w-12 h-12`) with the new `size-*` utility (e.g., `size-12`).

### Low Priority
- [ ] No low-priority tasks identified. The codebase is already in great shape.

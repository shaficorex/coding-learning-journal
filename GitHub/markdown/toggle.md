# Markdown Toggle (Collapsible Sections)

**Standard Markdown** does not provide a built-in toggle feature. On platforms that allow HTML inside Markdown, such as GitHub, collapsible sections can be created using the `<details>` and `<summary>` tags.

## Concept

- `<details>` creates a collapsible container.
- `<summary>` defines the visible title that users click to expand or collapse the content.
- Any Markdown content (text, lists, code blocks, etc.) can be placed inside the `<details>` section.

## Basic Structure

```html
<details>
<summary>Title</summary>

Hidden content goes here.

</details>
```

## Key Points

- The content inside `<details>` is hidden by default.
- Clicking the `<summary>` text expands or collapses the section.
- Adding the `open` attribute (`<details open>`) makes the section expanded by default.
- Useful for hiding long explanations, solutions, or large code blocks in documentation.

## Common Use Cases

- Organizing coding notes
- Hiding problem solutions
- Collapsing long explanations
- Structuring technical documentation in repositories on GitHub.

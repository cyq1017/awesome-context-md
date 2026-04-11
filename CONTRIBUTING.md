# Contributing to Awesome CONTEXT.md

Thank you for your interest in contributing! This project thrives on community input.

## Ways to Contribute

### 1. Add a Template

Create a new template for a project type we don't cover yet:

1. Choose a project type (e.g., `rust-cli`, `go-api`, `swift-ios`)
2. Create `templates/<type>.md` following the [CONTEXT.md spec](README.md#the-contextmd-spec)
3. Include placeholder comments like `<!-- Replace with your ... -->`
4. Submit a PR

### 2. Share Your CONTEXT.md

Share a real CONTEXT.md from your project:

1. **Sanitize** — Remove API keys, internal URLs, proprietary details
2. Create `examples/<project-name>.md`
3. Add a brief header explaining what the project does
4. Submit a PR

### 3. Improve Existing Templates

- Fix errors or unclear descriptions
- Add missing sections that you found useful
- Improve examples within templates

## Template Guidelines

A good template should:

- ✅ Follow the 7-section structure (What → Architecture → Tech Stack → Key Files → Conventions → State → Gotchas)
- ✅ Include `<!-- Replace with ... -->` placeholder comments
- ✅ Have a filled-in example section (not just empty placeholders)
- ✅ Be concise — aim for < 100 lines
- ❌ Not include real API keys, passwords, or proprietary information
- ❌ Not be overly generic — each template should reflect real patterns of its project type

## Code of Conduct

Be respectful. Be helpful. We're all here to make AI-assisted development better.

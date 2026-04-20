---
description: Review the changes in the current branch (or specified branch) and provide feedback.
---

# /review

Perform a comprehensive code review of all changes in the current branch (or specified branch) against master.

## Process

1. **Branch Diff Analysis**

    - Determine the name of the current branch to review
    - Run `git merge-base origin/master [branch]` to find the common ancestor commit
    - Run `git diff [common ancestor commit]..[branch]` to capture all changes in the branch
    - Identify all modified, added, and deleted files for comprehensive analysis

2. **File-by-File Code Review**

    - Read each modified file completely to understand context and changes
    - Focus on the specific diff sections but maintain awareness of surrounding code

## Review Standards

### Guidelines

- Be concise and specific - prioritize quality over quantity of feedback
- Provide **only** actionable feedback for all sections except "strengths"
    - Actionable feedback identifies specific issues that require code changes or improvements
    - Non-actionable feedback acknowledges good practices without suggesting changes
    - Example: "Missing error handling in submitForm() function" (actionable) vs "Good use of TypeScript types" (non-actionable)
    - Do not note what was changed in the actionable sections
    - Do not acknowledge good practices in the actionable sections
- Focus on reviewing the code
    - Do not run tests or linters
    - Do not make changes

### Repository-Specific Standards

#### Go Library (`zerolog-sentry`)
- This is a Go library providing a Sentry writer for `rs/zerolog`
- Error handling follows existing patterns — don't swallow errors, propagate with context
- Logging uses `rs/zerolog` — structured logging with appropriate levels
- Tests use standard library `testing` package with `stretchr/testify` assertions
- Linting via `golangci-lint`

### Code Quality Standards

- Includes appropriate tests (happy-path for new features, failing test for bugs)
- **CLAUDE.md impact**: update for new development patterns or commands
- **README impact**: update for new env vars, setup instructions, or dependencies
- **`go.mod` / `go.sum` changes**: correspond to actual dependency usage
- **Lint compliance**: changes must pass `make lint` and `make test`

### Suggestions Section

Focus on code quality improvements that enhance maintainability:

- Identify opportunities for code deduplication and suggest shared utilities
- Recommend opportunities to improve variable names, comments, & code organization
- Suggest performance optimizations that aren't critical issues
- Point out inconsistencies with existing patterns

## Output Format

Deliver structured feedback using this format:

```
## Code Review Results

### ✅ Strengths
[One concise sentence highlighting good practices and well-implemented features]

### 🚨 Critical Issues
[Must be fixed before merge. Each issue must include file_path:line_number]

- **[Issue Title]** (`file_path:line_number`) - [Specific problem and required fix]

### ⚠️ Important Issues
[Should be addressed. Each issue must include file_path:line_number]

- **[Issue Title]** (`file_path:line_number`) - [Specific problem and recommended fix]

### 💡 Suggestions
[Optional improvements that enhance code quality. Each must include file_path:line_number]

- **[Suggestion Title]** (`file_path:line_number`) - [Specific improvement opportunity]

**Overall Assessment:** [✅ Ready to merge | ⚠️ Needs revision | ❌ Critical issues must be resolved]
```

## Output Guidelines

- **Always include specific file paths with line numbers** for every item in actionable sections
- **Be direct and specific** about required changes - avoid vague feedback
- **Use bullet points** for multiple issues in the same category
- **Limit strengths to one sentence** - focus review time on actionable feedback
- **Omit empty sections** - if no critical issues exist, remove that section entirely
- **Do not include additional commentary** outside the specified format
- **Prioritize quality over quantity** - 3 specific issues are better than 10 vague ones

# No Assumptions Policy
You must NEVER make assumptions about:
- Implementation details not specified in the requirements
- Expected behavior or business rules
- API contracts or interfaces
- Data structures or formats
- Error handling approaches

## When faced with uncertainty:
1. **Search the codebase first** for existing patterns, similar implementations, or documentation
2. **Stop and ask explicit questions** if you cannot find clear answers
3. **Never proceed with guessed implementations**

## When to Stop and Ask
Stop immediately and ask questions when:
- The specification is ambiguous or incomplete
- You cannot find existing patterns for a required feature
- Multiple valid implementation approaches exist with no clear guidance
- Business rules or domain logic are unclear
- API contracts or interfaces are not defined
- Error handling requirements are not specified
- You're unsure which existing pattern to follow

# General guidelines
- Always put newline at the end of the files
- In comments, do not indicate what was the old behaviour. Comments should be agnostic to the timeline of your changes
- If you are extracting some common implementation, ensure it is being used in all places

# Go guidelines
- Error handling: Always check nil errors. Propagate with context using fmt.Errorf
- Testing: Never use skip in tests. Use standard library `testing` package with `stretchr/testify` assertions
- Linting: Run `make lint` to check code quality
- Testing: Run `make test` to run tests with race detection
- Formatting: Run `go fmt ./...` before committing

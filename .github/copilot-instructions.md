# Easy Kit Utils - GitHub Copilot Instructions

## Project Overview
**Easy Kit Utils** is an open source JavaScript/TypeScript library that provides common and reusable utilities to simplify development. The project was created by DomeT99 (Domenico Tenace) as a collection of lightweight, performant, and well-tested validation and checking functions.

**Repository**: https://github.com/DomeT99/easy-kit-utils  
**NPM Package**: https://www.npmjs.com/package/easy-kit-utils  
**License**: MIT

## Core Technologies & Stack

### Runtime & Build
- **Bun** - JavaScript runtime and build tool (package manager)
- **TypeScript** - Primary programming language (v5.0+)
- **ESNext** - Compilation target for maximum compatibility with modern browsers

### Testing & Quality Assurance
- **Jest** - Testing framework (v29.7.0)
- **@jest/globals** - Global test utilities

### Module System
- **ES Modules (ESM)** - Contemporary module system
- **CommonJS compatibility** - Dual export for backward compatibility

## Project Structure & Organization

```
easy-kit-utils/
├── src/
│   ├── index.ts                 # Main entry point exporting all utilities
│   └── checkUtils/
│       ├── index.ts             # Barrel export for checkUtils
│       ├── isArray/
│       │   ├── isArray.ts       # Function implementation
│       │   └── isArray.test.ts  # Unit tests
│       ├── isBlankArray/        # Empty/null array check
│       ├── isEmptyString/       # Empty string check
│       ├── isMajorNumber/       # Greater than check
│       ├── isMajorSameNumber/   # Greater or equal check
│       ├── isMinorNumber/       # Less than check
│       ├── isMinorSameNumber/   # Less or equal check
│       ├── isNull/              # Null check
│       ├── isTrue/              # True check
│       └── isUndefined/         # Undefined check
├── dist/                        # Compiled output (generated)
├── package.json                 # Project configuration and dependencies
├── tsconfig.json                # TypeScript configuration
├── bun.lockb                    # Lock file for Bun dependencies
└── README.md                    # Project documentation
```

## Architecture & Design Principles

### Design Philosophy
- **Extreme Simplicity**: Functions with single responsibility
- **Zero Dependencies**: No external dependencies (except Jest for testing)
- **Type Safety**: Full TypeScript support with generics where appropriate
- **Performance First**: Lightweight and optimized functions
- **Well Tested**: Complete test coverage for every utility

### Design Pattern
Utility functions follow a consistent pattern:
1. Each function resides in a dedicated folder: `src/checkUtils/{functionName}/`
2. Contains two files: `{functionName}.ts` (implementation) and `{functionName}.test.ts` (tests)
3. Each function is exported from the category's `index.ts` file
4. All functions are then exported from the main `src/index.ts`

## Available Utilities (checkUtils)

### Array Validation
- **`isArray<T>(param: T): boolean`** - Verifies if the parameter is an array
- **`isBlankArray<T>(param: T[]): boolean`** - Verifies if array is empty or null

### String Validation
- **`isEmptyString(param: string): boolean`** - Verifies if string is empty

### Boolean Validation
- **`isTrue(param: boolean): boolean`** - Verifies if value is true

### Null/Undefined Checks
- **`isNull(param: unknown): boolean`** - Verifies if value is null
- **`isUndefined(param: unknown): boolean`** - Verifies if value is undefined

### Numeric Comparisons
- **`isMajorNumber(paramFirst: number, paramSecond: number): boolean`** - Verifies if `paramFirst > paramSecond`
- **`isMajorSameNumber(paramFirst: number, paramSecond: number): boolean`** - Verifies if `paramFirst >= paramSecond`
- **`isMinorNumber(paramFirst: number, paramSecond: number): boolean`** - Verifies if `paramFirst < paramSecond`
- **`isMinorSameNumber(paramFirst: number, paramSecond: number): boolean`** - Verifies if `paramFirst <= paramSecond`

## TypeScript & Code Style

### TypeScript Configuration
- **Target**: ESNext - for compatibility with modern runtimes
- **Module**: ESNext - standard ES6+ modules
- **Lib**: ESNext + DOM - support for current features
- **Strict Mode**: Enabled (`strict: true`) for maximum type safety
- **verbatimModuleSyntax**: Enabled - preserves original module syntax

### Code Conventions
- Use **generics** where appropriate (e.g., `isArray<T>`) for maximum type flexibility
- Follow **Strict Type Checking**
- Prefer **type safety** over development convenience
- Use **JSDoc comments** to document complex functions
- Maintain **explicit names** for functions and parameters
- Follow **camelCase** for function and variable names
- Use **PascalCase** for types and interfaces

## Build & Distribution

### Available Scripts
```bash
# Compile the library
bun run publish

# Run tests
bun run test
# or alternative
npm run test
```

### Export Configuration
- **main**: `./dist/index.js` - Main entry point
- **module**: `./dist/index.js` - ESM entry point
- **exports**: Dual configuration for import/require
- **type**: `module` - Specifies ESM as default

### Build Process
1. Source files in `src/`
2. TypeScript compilation with Bun: `bun build src/index.ts --outdir ./dist`
3. Output in `dist/index.js`
4. Distribution via NPM

## Testing Guidelines

### Framework and Setup
- **Jest** as test runner
- **@jest/globals** for describe, test, expect
- Each function must have corresponding `{functionName}.test.ts` file

### Test Pattern
```typescript
import { describe, expect, test } from "@jest/globals";
import { functionName } from "./functionName";

describe("functionName suite tests", () => {
  test("return true", () => {
    expect(functionName(value)).toBe(true);
  });

  test("return false", () => {
    expect(functionName(value)).toBe(false);
  });
});
```

### Best Practices for Testing
- At least one test for "true" case and one for "false" case
- Use clear and specific descriptions
- Test edge cases when relevant
- Keep tests simple and focused
- One assertion per test when possible

## Adding New Utilities

### When to Add a New Utility
- The function solves a common and reusable problem
- It has no external dependencies
- It maintains simplicity and code clarity
- It follows the project's type safety pattern

### Addition Process
1. Create folder: `src/checkUtils/{newFunctionName}/`
2. Create implementation file: `{newFunctionName}.ts`
   - Export function with explicit export statement
   - Use TypeScript with complete type hints
   - Include JSDoc if necessary
3. Create test file: `{newFunctionName}.test.ts`
   - Cover at least the main cases
   - Follow the standardized Jest pattern
4. Update `src/checkUtils/index.ts` with the new export
5. Export from main `src/index.ts` will happen automatically

### Example of New Function
```typescript
// src/checkUtils/isPositiveNumber/isPositiveNumber.ts
export function isPositiveNumber(param: number): boolean {
  if (param > 0) {
    return true;
  }
  return false;
}
```

```typescript
// src/checkUtils/isPositiveNumber/isPositiveNumber.test.ts
import { describe, expect, test } from "@jest/globals";
import { isPositiveNumber } from "./isPositiveNumber";

describe("isPositiveNumber suite tests", () => {
  test("return true for positive number", () => {
    expect(isPositiveNumber(5)).toBe(true);
  });

  test("return false for zero", () => {
    expect(isPositiveNumber(0)).toBe(false);
  });

  test("return false for negative number", () => {
    expect(isPositiveNumber(-5)).toBe(false);
  });
});
```

## Modifying Existing Functions

### Important Considerations
- Maintain **backward compatibility** when possible
- Update both implementation and tests
- If function signature changes, consider a version bump (SEMVER)
- Document changes in README.md and commit

### Process
1. Modify the implementation `.ts` file
2. Update or extend the `.test.ts` file
3. Run tests: `bun run test`
4. Verify build: `bun run publish`

## NPM Package Management

### Versioning
- Follow **Semantic Versioning** (MAJOR.MINOR.PATCH)
- Package.json contains current version (currently v0.0.2)
- Increment version in package.json before publishing

### Publishing
- Build: `bun run publish` generates `dist/index.js`
- NPM configuration in package.json
- Distribution via NPM registry

## Quality & Performance Considerations

### Code Quality
- Use TypeScript strict mode
- Zero linting errors
- Descriptive and clear names
- Pure functions (no side effects when possible)

### Performance
- Lightweight and optimized functions
- Zero unnecessary memory allocations
- Prefer native JavaScript implementations
- Avoid complex loops and operations

### Maintainability
- Self-documenting code
- JSDoc for complex logic
- Clear and explicit test descriptions
- Modularity and separation of concerns

## Development Workflow

### Local Setup
```bash
# Install dependencies
bun install

# Run tests
bun run test

# Build
bun run publish
```

### During Development
1. Create/modify files in `src/` folder
2. Keep tests updated
3. Run tests locally
4. Verify the build

### Before Commit
1. Run all tests: `bun run test`
2. Run build: `bun run publish`
3. Verify that dist/ is updated
4. Check for TypeScript errors

## Repository and Contribution

### Repository Info
- **Owner**: DomeT99
- **License**: MIT (open source)
- **Main Branch**: main
- **Package Manager**: Bun

### Contribution Guidelines
- Maintain the simplicity philosophy
- Follow the project's structure pattern
- Provide complete tests for new functions
- Document significant changes
- Respect type safety principles

## Author & Support

- **Author**: Domenico Tenace (DomeT99)
- **Contact**: domenicotenace99@gmail.com
- **Links**: https://linktr.ee/domenicotenace
- **Support**: Those who appreciate the project can support with donations

## Notes for AI Assistant
- Maintain **simplicity and clarity** in all suggestions
- Emphasize **type safety** and **performance**
- Respect the existing project structure
- Every new utility must add real value
- Prefer **small focused functions** over monolithic functions
- Always run tests before any modifications
- Maintain **compatibility with modern runtimes** (Bun, Node.js, Browser)
- No external dependencies unless absolutely necessary
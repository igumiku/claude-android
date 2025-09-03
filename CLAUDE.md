> You are an expert Android engineer specializing in Kotlin, Jetpack Compose, and modern app architecture. Respond with production-ready, idiomatic Kotlin code. Always follow Android best practices and explain tradeoffs briefly when necessary.

# CLAUDE.md - Android Project Automation

## System Instructions
- By default, all commands are automatically approved and executed.
- Any command starting with `ask:` must **pause and request user confirmation** before executing.
- Commands can be grouped by type: `commit:`, `deploy:`, `feature:`, `ask:`. Only `ask:` requires manual approval.
- Never execute `ask:` commands without explicit user confirmation.
- Always show the user the command to be executed, even for auto-approved commands.

---

## Command Examples

### Auto-Approved Commands
- commit: update README automatically
- commit: sync project dependencies
- deploy: deploy to staging environment
- feature: create new Compose UI skeleton
- feature: generate mock data

### Manual Approval Commands
- ask: delete production database
- ask: drop old migration table
- ask: force reset feature branch
- ask: remove user data folder

---

## Notes for Claude Code
- You may encounter commands in the future that require approval; always check for the `ask:` prefix.
- Commands without any prefix default to **auto-approve**.
- Ensure any executed command logs the result or shows confirmation after execution.


# Claude Code Context: Android Development

## Goal
I’m building and maintaining Android applications. Please provide concise, production-grade solutions in Kotlin and Android best practices. Explanations should be clear but not overly verbose.

---

## Preferred Tech Stack
- **Programming Language**: Kotlin
- **Build System**: Gradle (KTS preferred)
- **UI Framework**: Jetpack Compose
- **Architecture**: MVVM or Clean Architecture
- **Dependency Injection**: Hilt/Dagger
- **Coroutines**: For async and concurrency
- **Navigation**: Jetpack Navigation
- **Persistence**: Room or DataStore
- **Networking**: Retrofit + OkHttp
- **Testing**: JUnit, Espresso, MockK

---

## Guidelines for Code Generation
1. Always use **Kotlin idioms** (extension functions, sealed classes, coroutines, etc.).
2. Favor **Jetpack Compose** for UI unless XML is explicitly required.
3. Show **full working examples** where possible (imports included).
4. Ensure **Gradle setup instructions** if adding libraries.
5. Use **best practices**:
    - Separation of concerns
    - Single source of truth
    - Lifecycle-aware components
6. Assume **Android Studio Giraffe+** and **Gradle 8+**.
7. If multiple solutions exist, **recommend the modern approach** first.

---

## Example Prompts I Might Ask
- “Create a Jetpack Compose screen with a list of items from a REST API.”
- “Explain how to use coroutines and flows for reactive data.”
- “Generate a Gradle dependency block for Retrofit and Hilt.”
- “Write an Espresso test for a Compose UI.”

---

## My Preferences
- Prioritize **readability over cleverness**.
- Prefer **dependency injection** for testability.
- Minimize boilerplate.
- Explain tradeoffs if relevant.

---

## Don’ts
- Don’t use deprecated APIs.
- Don’t write Java unless asked.
- Don’t skip imports in examples.

This is a large-scale Android project using Gradle with Kotlin DSL. Common build commands:

- `./gradlew build` - Build the entire project
- `./gradlew app:assembleDebug` - Build debug APK for the main app
- `./gradlew app:assembleProdDebug` - Build debug APK for production flavor
- `./gradlew clean` - Clean build outputs

## Testing Commands

- `./gradlew test` - Run unit tests for all modules
- `./gradlew app:test` - Run unit tests for the app module only
- `./gradlew connectedAndroidTest` - Run instrumented tests (requires device/emulator)
- `./gradlew app:connectedProdDebugAndroidTest` - Run instrumented tests for specific flavor

## Code Quality Commands

- `./gradlew ktlintCheck` - Check Kotlin code style across all modules
- `./gradlew ktlintFormat` - Auto-format Kotlin code across all modules
- `./gradlew app:ktlintCheck` - Check specific module
- `./gradlew app:ktlintFormat` - Format specific module
- `./gradlew app:lint` - Run Android lint checks

## State management
- Use Hilt to generate viewmodel to manage state for compose ui if the ui component need to be stateful

### Key Architectural Patterns
- Uses Hilt for dependency injection
- Compose UI with traditional View system
- Multi-module architecture with clear boundaries

## Project Structure

- `app/src/main/java/com/example/myapplication/` - Main application code
    - `MainActivity.kt` - Main entry point using ComponentActivity with Compose
    - `ui/theme/` - Material 3 theming with dark/light mode support and dynamic colors
- `app/src/test/` - Unit tests using JUnit
- `app/src/androidTest/` - Instrumented tests using AndroidX Test
- `gradle/libs.versions.toml` - Centralized dependency management using version catalogs

## Architecture Notes

- Uses Jetpack Compose for UI with Material 3 design system
- Implements edge-to-edge design with proper insets handling
- Theme system supports dynamic colors (Android 12+) and dark/light modes
- Standard Android single-activity architecture with Compose navigation ready


# Feature Development Workflow for Android (Kotlin + Compose)

This Claude.md defines the full workflow for developing a new feature. The workflow is **approval-driven**: Claude must pause and ask for approval at every step before proceeding.

---

## Workflow Steps

### 0. Feature Initialization
- Create a feature branch: `feature/<feature-name>`
- Ask: "Do you want to start this feature? (yes/no)"
- Wait for my approval.

---

### 1. PRD Creation
- Create folder: `/prd/`
- Create file: `/prd/README.md`
- Draft PRD content including:
    - Feature purpose and goals
    - User stories
    - Acceptance criteria
    - Optional UI mockups
- Ask: "Do you approve this PRD? (yes/no)"
- Wait for approval.
- Generate git commands for adding and committing:

---

### 2. High-Level Technical Design
- Create folder: `/design/high_level/`
- Create files:
- `/design/high_level/architecture.md`
- `/design/high_level/components.md`
- Draft high-level design content:
- System architecture diagram
- Component interactions
- API/interface plan
- Data flow
- Ask: "Do you approve the high-level design? (yes/no)"
- Wait for approval.
- Generate git commands for commit.

---

### 3. Low-Level Design
- Create folder: `/design/low_level/`
- Create files:
- `classes.md`
- `data_models.md`
- `ui_structure.md`
- Draft content:
- Classes, data models, modules
- Function signatures
- UI structure & state management
- Database schema changes (if any)
- Ask for approval.
- Generate git commands.

---

### 4. Test Plan
- Create folder: `/tests/`
- Create file: `/tests/test_plan.md`
- test case need to cover the PRD context in /PRD
- generated test case and verifycation should depend on the PRD also
- Draft test cases:
- Unit tests
- Integration tests
- UI / Compose tests
- Edge cases
- Pause and ask for approval.
- Generate git commands.

---

### 5. Task Split & PR Plan
- Create folder: `/tasks/`
- Create file: `/tasks/task_list.md`
- Draft task breakdown:
- Task name, description, target files
- PR branch name: `task/<feature-name>/<task-name>`
- Example git commands for creating task branch and PR
- Ask: "Do you approve the task & PR plan? (yes/no)"
- Pause for approval.

---

### 6. Implement Each Task
- For each task:
1. Create task branch: `task/<feature>/<task-name>`
2. Add initial files/code according to low-level design
3. Add test files/cases base the test plan
4. build and run to check if compile error
5. run to check if unit test pass
6. run to check if e2e test pass
7. Ask: "Do you approve this task implementation and tests? (yes/no)"
8. Only after approval → commit & push

---

### 7. Final Integration
- Merge all task branches into the feature branch
- Run full test suite
- Ask: "Do you approve final feature integration? (yes/no)"
- Merge to `main` only after approval
- Commit final integration.

---

### 8. build and run the app
- run all the unit tests and androidTest and verify all the tests
- build: ./gradlew assembleDebug
- start an emulator by commanline
- install app by adb: adb install -r
- run the app by adb: adb shell am start -n

---

## Rules for Claude
1. **Do not proceed** without explicit “yes” from the user.
2. All changes must create actual folders/files in the project.
3. Fill files with draft content relevant to the step.
4. Generate git commands for adding and committing changes.
5. Keep a **summary table** of all steps and their approval status.
6. Each commit must be **atomic and verifiable**.

# build system for android project

## Build Commands

```bash
# Build the project
./gradlew build

# Build debug APK
./gradlew assembleDebug

# Build release APK
./gradlew assembleRelease

# Clean build
./gradlew clean
```

## Testing Commands

```bash
# Run unit tests
./gradlew test

# Run instrumented tests (requires Android device/emulator)
./gradlew connectedAndroidTest

# Run all tests
./gradlew check
```


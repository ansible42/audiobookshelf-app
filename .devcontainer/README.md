Devcontainer for Audiobookshelf Mobile App

Usage
- Open this repository in VS Code and choose "Reopen in Container" when prompted.
- The container provides Node 20, OpenJDK 11, Gradle and Android SDK command-line tools.
- A `postCreateCommand` runs `npm install` automatically.

Common tasks (from VS Code Tasks palette):
- `npm: install` — installs Node dependencies
- `Generate (nuxt)` — runs `npm run generate` to build the web assets
- `Capacitor: sync` — runs `npx cap sync` to copy the web assets into the native projects
- `Open Android (Android Studio)` — runs `npx cap open android`

Notes
- Building iOS requires macOS tooling (Xcode); iOS builds are not supported inside this Linux container.
- If you need a specific Android platform or build-tools, update the Dockerfile sdkmanager invocation.

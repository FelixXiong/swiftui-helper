---
name: "swiftui-helper"
description: "Reads SwiftUI, Swift, and Apple platform documentation, scans latest APIs, and looks up official Apple docs. Invoke when user asks about SwiftUI APIs, Swift syntax, Xcode compilation errors, new Apple framework features, or needs to check for API updates."
author: "Penghao Xiong,Zhaoxian Dong"
version: "1.0.0"
organization: "Mensheng Studio"
license: "MIT"
version: "1.0.0"
---

# SwiftUI Documentation Helper

This skill helps you read and query SwiftUI, Swift, and Apple platform documentation from both local project documents and official online sources. It also scans and learns the latest Apple SDK documentation.

## When to Invoke

**Invoke this skill IMMEDIATELY when:**

- User asks about SwiftUI APIs or framework usage
- User encounters Swift or Xcode compilation errors
- User needs to understand SwiftUI views, modifiers, or navigation
- User asks about iOS/macOS/watchOS/tvOS capabilities or frameworks
- User needs to look up official Apple documentation
- User asks questions like "how to use X in SwiftUI" or "what is the correct API for Y"
- User asks about new SwiftUI APIs or WWDC features
- User wants to check for API updates
- User asks "what's new in iOS X / SwiftUI X"
- User encounters an API that might be deprecated or changed
- User wants to learn about the latest SDK capabilities
- User asks about Swift concurrency, Combine, Observation, or App Intents
- User asks about SwiftData, Core Data, or persistence APIs

## Invocation Rule

This skill is triggered when user queries involve:

- SwiftUI UI construction
- iOS API usage
- Xcode compilation errors
- Apple framework lookup

## Local Documentation Sources

The project maintains comprehensive local documentation:

### Primary Documents

| Document | Path | Content |
| --------------------------------| ----------------------------------- | -------------------------------------- |
| SWIFTUI_COMPLETE_GUIDE.md | `/SWIFTUI_COMPLETE_GUIDE.md` | Complete SwiftUI development guide |
| SWIFT_COMPILER_ERRORS.md | `/SWIFT_COMPILER_ERRORS.md` | Compilation error solutions |
| 技术文档.md | `/docs/技术文档.md` | Technical issue solutions |
| ios/README.md | `/docs/ios/README.md` | iOS development index |

### Key Topics Covered Locally

- NavigationStack / NavigationPath usage
- ObservableObject vs @Observable
- SwiftData model container issues
- Async/await concurrency patterns
- MainActor threading issues
- View lifecycle and state management
- Property wrapper conflicts
- Environment and dependency injection
- Image loading and AsyncImage
- Sheet / fullScreenCover presentation patterns
- Gesture APIs and animation updates
- Swift Package Manager integration
- UIKit interoperability with UIViewRepresentable
- FileImporter / PhotosPicker usage
- **NEW**: Observation framework migration
- **NEW**: SwiftData relationships and queries
- **NEW**: iOS 18 navigation transition APIs
- **NEW**: GlassEffectContainer and Liquid Glass
- **NEW**: @Bindable usage patterns
- **NEW**: AppIntent and Widget configuration
- **NEW**: Swift macros and attached macros
- **NEW**: Result builder type inference issues
- **NEW**: "Type of expression is ambiguous" fixes
- **NEW**: Preview macro (`#Preview`) migration
- **NEW**: Sendable and actor isolation errors

## Online Documentation Sources

When local docs are insufficient, query official sources:

### Primary Online Resources

1. Apple Developer Documentation: https://developer.apple.com/documentation/
2. SwiftUI Documentation: https://developer.apple.com/documentation/swiftui
3. Swift Documentation: https://docs.swift.org/swift-book/documentation/the-swift-programming-language/
4. WWDC Videos: https://developer.apple.com/videos/
5. Human Interface Guidelines: https://developer.apple.com/design/human-interface-guidelines/

### Search Strategy

1. First check local documentation for known issues
2. Use WebSearch for specific API questions
3. Use WebFetch for detailed documentation pages
4. Check WWDC sessions for latest framework updates

## Usage Examples

### Example 1: Compilation Error

```
User: "I got 'Type of expression is ambiguous without a type annotation'"
Action: Read SWIFT_COMPILER_ERRORS.md, find the error section, provide solution
```

### Example 2: API Usage

```
User: "How to use PhotosPicker in SwiftUI?"
Action:
1. Check local docs for PhotosPicker examples
2. If not found, search Apple docs
3. Provide code example with explanation
```

### Example 3: Navigation Migration

```
User: "NavigationView is deprecated?"
Action: Explain NavigationStack migration and provide updated examples
```

## Response Format

When answering documentation questions:

- **Cite Sources**: Always mention where the information comes from
  - "According to local docs at [path]..."
  - "From official Apple documentation..."
- **Provide Code Examples**: Include working Swift code snippets
- **Explain Context**: Why this API/pattern exists, when to use it
- **Link to Details**: Provide clickable links to relevant sections

## Common Quick References

### NavigationStack

```swift
struct ContentView: View {
    @State private var path = NavigationPath()

    var body: some View {
        NavigationStack(path: $path) {
            List {
                Button("Go Detail") {
                    path.append("detail")
                }
            }
            .navigationDestination(for: String.self) { value in
                DetailView(value: value)
            }
        }
    }
}
```

### Observable vs ObservableObject

```swift
import Observation

@Observable
class UserStore {
    var name: String = ""
    var age: Int = 0
}
```

### AsyncImage

```swift
AsyncImage(url: URL(string: imageURL)) { image in
    image
        .resizable()
        .scaledToFill()
} placeholder: {
    ProgressView()
}
```

### PhotosPicker

```swift
import PhotosUI

@State private var selectedItem: PhotosPickerItem?
@State private var selectedImage: Image?

PhotosPicker(
    selection: $selectedItem,
    matching: .images
) {
    Label("Select Photo", systemImage: "photo")
}
.task(id: selectedItem) {
    if let data = try? await selectedItem?.loadTransferable(type: Data.self),
       let uiImage = UIImage(data: data) {
        selectedImage = Image(uiImage: uiImage)
    }
}
```

### SwiftData Model

```swift
import SwiftData

@Model
class Note {
    var title: String
    var createdAt: Date

    init(title: String) {
        self.title = title
        self.createdAt = Date()
    }
}
```

### File Importer

```swift
.fileImporter(
    isPresented: $showImporter,
    allowedContentTypes: [.image]
) { result in
    switch result {
    case .success(let url):
        print(url)
    case .failure(let error):
        print(error)
    }
}
```

### MainActor Fixes

```swift
@MainActor
class ViewModel: ObservableObject {
    @Published var items: [String] = []

    func load() async {
        items = await fetchData()
    }
}
```

### Preview Macro

```swift
#Preview {
    ContentView()
}
```

### Glass Effect (iOS 26+)

```swift
GlassEffectContainer {
    VStack {
        Text("Hello")
    }
}
```

## Latest API Scanning

When user asks about new APIs or features, follow this process:

### Step 1: Check Current SDK Version

```swift
// Check project.pbxproj or Package.swift
// Check deployment target and Xcode SDK version
```

### Step 2: Scan for New APIs

Use WebSearch to find:

```
site:developer.apple.com SwiftUI iOS 26 new APIs
site:developer.apple.com WWDC SwiftUI updates
site:developer.apple.com deprecated SwiftUI APIs
```

### Step 3: Fetch Detailed Documentation

For each new API found, fetch:

- API signature and parameters
- Usage examples
- Platform requirements
- Breaking changes
- Migration guidance

### Step 4: Update Local Documentation

Update the following local files:

- `/SWIFTUI_COMPLETE_GUIDE.md` - Add new API patterns
- `/SWIFT_COMPILER_ERRORS.md` - Add new error types
- `/docs/技术文档.md` - Add technical solutions

## SDK Version Mapping

| iOS Version | SwiftUI Version | Key Features |
|------------|-----------------|---------------|
| iOS 26+ | SwiftUI 6.0 | Liquid Glass, GlassEffectContainer, Advanced symbol animations |
| iOS 18+ | SwiftUI 5.0 | Observation framework, SwiftData improvements, Navigation redesign |
| iOS 17+ | SwiftUI 4.0 | @Observable, SwiftData, #Preview macro |
| iOS 16+ | SwiftUI 3.0 | NavigationStack redesign, Grid improvements |
| iOS 15+ | SwiftUI 2.0 | AsyncImage, PhotosPicker, structured concurrency |

## New APIs to Watch

### iOS 26+

```swift
// Liquid Glass
GlassEffectContainer {
    content
}

// Advanced symbol animations
Image(systemName: "heart.fill")
    .symbolEffect(.bounce)
```

### iOS 17+

```swift
// Observation
@Observable
class SettingsStore {
    var theme: Theme = .system
}

// SwiftData
@Query(sort: \Note.createdAt)
private var notes: [Note]
```

### Swift Concurrency

```swift
Task {
    await loadData()
}

async let profile = fetchProfile()
async let posts = fetchPosts()

let result = await (profile, posts)
```

## API Scanning Output Format

When reporting new APIs, use this format:

```markdown
## 🆕 New API: [API Name]

**Version**: iOS XX / SwiftUI XX
**Framework**: `SwiftUI` / `Foundation`
**Status**: New / Updated / Deprecated

### Signature

```swift
[API signature]
```

### Usage Example

```swift
[Code example]
```

**Requirements**:
- Minimum iOS version: XX
- Platform support: iPhone / iPad / Mac / Vision Pro

### Migration Notes

[If replacing old API, explain how to migrate]
```

## Common Search Patterns

### Find New Components

```
site:developer.apple.com SwiftUI new views
```

### Find API Changes

```
site:developer.apple.com SwiftUI deprecated APIs
```

### Find WWDC Sessions

```
site:developer.apple.com WWDC SwiftUI session
```

## Local Documentation Update Rules

- **New API**: Add to SWIFTUI_COMPLETE_GUIDE.md with usage example
- **Breaking Change**: Add to SWIFT_COMPILER_ERRORS.md with migration guide
- **Deprecation**: Add warning to relevant sections
- **New Pattern**: Add to TECHNICAL_DOCS.md with solution

All API information is retrieved from Apple official documentation sources and may be subject to SDK version differences.

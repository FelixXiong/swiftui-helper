## Metadata

- Author: Penghao Xiong,Zhaoxian Dong
- Version: 1.0.0
- Organization: Mensheng Studio
- License: MIT

# SwiftUI Helper

A SwiftUI + Apple Developer documentation intelligence skill for iOS development.

Designed for:
- SwiftUI development assistance
- API lookup and migration guidance
- Xcode error debugging

A versatile assistant for reading SwiftUI, Swift, and Apple platform documentation from both local project documents and official online sources. Works across Trae IDE, Visual Studio Code, Xcode, and integrates with AI assistants like Claude, CodeLlama, and GitHub Copilot.

## Overview

SwiftUI Helper provides comprehensive documentation assistance for Apple platform UI development using SwiftUI framework. It includes local documentation lookup, official Apple docs access, and latest API scanning capabilities—accessible through any IDE or AI coding assistant.

## Problem

Developers often struggle to quickly locate correct SwiftUI / Apple API usage across fragmented documentation sources, especially when dealing with version differences and deprecations.

## Solution

This Skill provides structured retrieval of Apple Developer documentation with:
- Version-aware API lookup
- SwiftUI-first navigation patterns
- Context-aware code snippets

## Features

### Documentation Sources

- **Local Documentation**: Complete guides, compilation error solutions, and technical issue documentation
- **Online Documentation**: Apple Developer Docs, Swift.org, WWDC videos, Human Interface Guidelines
- **Latest API Updates**: Scans and reports new SwiftUI APIs from Apple

### Core Capabilities

- SwiftUI View generation and templates
- State management patterns (@State, @Binding, @Observable, @EnvironmentObject)
- Layout system guidance (NavigationStack, VStack, HStack, ZStack, LazyVGrid)
- SwiftData and persistence APIs
- Swift Concurrency (async/await, actors, MainActor)
- Image loading (AsyncImage, PhotosPicker)
- FileImporter and document handling
- Swift macros and attached macros
- Compilation error resolution
- API migration guides (NavigationView → NavigationStack)

### SDK Version Support

| iOS Version | SwiftUI Version | Key Features |
|------------|-----------------|---------------|
| iOS 26+ | SwiftUI 6.0 | Liquid Glass, GlassEffectContainer |
| iOS 18+ | SwiftUI 5.0 | Observation framework, SwiftData improvements |
| iOS 17+ | SwiftUI 4.0 | @Observable, SwiftData, #Preview macro |

## Usage

This helper works seamlessly across various IDEs and AI assistants. Simply describe what you want to build or the problem you're facing.

### Example Triggers

- "How do I use NavigationStack in SwiftUI?"
- "What's the difference between @Observable and @ObservableObject?"
- "How to fix 'Type of expression is ambiguous' error"
- "What's new in iOS 18 SwiftUI?"
- "How to use SwiftData in my app?"
- "Explain Swift concurrency in SwiftUI"

### IDE & AI Assistant Integration Examples

**Trae IDE:**
```
User: "帮我实现一个 SwiftUI 列表视图"
→ Skill automatically retrieves NavigationStack examples from local docs
```

**Visual Studio Code with GitHub Copilot:**
```
User: "@Copilot, show me how to use AsyncImage in SwiftUI"
→ Integrates with this helper to provide accurate code snippets
```

**Claude 3.5 Sonnet:**
```
User: "Claude, explain how to migrate from @ObservableObject to @Observable"
→ Uses this documentation helper to provide version-aware guidance
```

**Xcode with CodeLlama:**
```
User: "/explain SwiftData @Query usage"
→ Leverages local docs for context-aware explanations
```

**JetBrains AppCode:**
```
User: "Show me how to implement PhotosPicker in iOS 18"
→ Provides version-specific API examples
```

## Requirements

- Swift 5.9+
- Xcode 15.0+
- Apple platform target (iOS 17+, macOS 14+, watchOS 10+, tvOS 17+)

## Local Documentation Files

The skill maintains comprehensive local documentation:

- `SWIFTUI_COMPLETE_GUIDE.md` - Complete SwiftUI development guide
- `SWIFT_COMPILER_ERRORS.md` - Compilation error solutions
- `docs/技术文档.md` - Technical issue solutions
- `docs/ios/README.md` - iOS development index

## Documentation Format

When providing answers, the skill will:

1. Cite sources (local docs or official Apple documentation)
2. Provide working Swift code examples
3. Explain context and usage scenarios
4. Link to relevant documentation sections

For detailed technical specifications, see [skill.md](./skill.md).

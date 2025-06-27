# CLAUDE.md

This file provides guidance to Claude Code (claude.ai/code) when working with code in this repository.

## Development Commands

This is a **zero-dependency static web application** - no build system or package manager required.

**Development workflow:**
- Edit `index.html` directly - the entire application is in this single file
- Refresh browser to see changes
- Open `index.html` directly in browser for local testing

**No common commands like npm/yarn scripts** - this is intentional to keep the app dependency-free and highly portable.

## Architecture Overview

**Single-file architecture**: The entire application (HTML, CSS, JavaScript) is contained in `index.html`. This design choice prioritizes:
- Zero external dependencies
- Maximum portability and deployment simplicity  
- Direct browser compatibility without build steps

**Core application structure:**
- **Tab-based SPA**: Session, Progress, Insights, Settings tabs with JavaScript navigation
- **State management**: Global JavaScript variables with localStorage persistence
- **Timer-driven sessions**: Complex multi-phase breathing cycles using setInterval/setTimeout
- **Canvas-based charts**: Custom progress visualization without charting libraries

**Key JavaScript modules within the single file:**
- **Session Management**: `startSession()`, breathing phase controllers, timer orchestration
- **Data Persistence**: LocalStorage wrapper functions for session history and settings
- **UI Controllers**: Tab switching, modal dialogs, breathing visualizer animations
- **Analytics Engine**: Performance calculations, streak tracking, trend analysis

**Data architecture:**
- Sessions stored as JSON in localStorage key `whmSessions`
- Settings stored as JSON in localStorage key `whmSettings`
- No external database - completely client-side data management

## Key Implementation Details

**Browser API Integration:**
- **Web Speech API**: Voice guidance with `speechSynthesis` (optional feature)
- **Canvas 2D API**: Progress charts and data visualization
- **Vibration API**: Mobile haptic feedback during breathing phases
- **LocalStorage API**: Complete data persistence layer

**CSS Architecture:**
- **Responsive design**: CSS Grid and Flexbox with mobile-first approach
- **Animation system**: CSS keyframes for breathing visualizer, no JavaScript animation libraries
- **Custom properties**: CSS variables for theming and dynamic styling

**Timer Management Pattern:**
The application uses a complex timer orchestration system:
- Multiple concurrent intervals for different UI updates
- Phase-based session management (breathing → hold → recovery)
- Cleanup functions critical to prevent memory leaks when stopping sessions

**Mobile Optimization:**
- Touch-friendly interface with appropriate button sizing
- Responsive breakpoints for various screen sizes
- Vibration feedback for breathing cues on mobile devices

## Safety and UX Considerations

The app implements breathing exercise training with built-in safety features:
- Emphasis on "comfortable holds" vs maximum breath holding
- Safety warnings integrated into the UI
- Session parameters limited to safe ranges (1-10 rounds, 20-40 breaths)

When modifying session logic or timer management, maintain these safety-first principles and ensure timer cleanup to prevent runaway intervals.
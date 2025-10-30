# 🍅 Pomdo

<div align="center">

![Go](https://img.shields.io/badge/go-1.21+-00ADD8.svg)
![CLI](https://img.shields.io/badge/CLI-Terminal-green.svg)
![Pomodoro](https://img.shields.io/badge/Pomodoro-Technique-red.svg)
![License](https://img.shields.io/badge/license-MIT-blue.svg)

**A beautiful, terminal-based Pomodoro Timer built with Go and Bubble Tea**

*Boost your productivity with the Pomodoro Technique in your terminal*

</div>

---

## 🌟 Features

- **🎨 Beautiful TUI**: Styled terminal interface using Bubble Tea and Lip Gloss
- **⏱️ Full Pomodoro Cycle**: Work sessions, short breaks, and long breaks
- **🔄 State Management**: Automatic phase transitions with visual feedback
- **⌨️ Keyboard Controls**: Intuitive keybindings for all actions
- **🎯 Progress Tracking**: Visual progress indicators and session counters
- **🎨 Theme Support**: Color-coded phases and responsive design
- **📊 Statistics**: Track completed sessions and productivity metrics

## 🏗️ Architecture Overview

```
┌─────────────────────────────────────────┐
│               Pomdo CLI                 │
├─────────────────────────────────────────┤
│  🎨 View Layer (Lip Gloss Styling)     │
│  ├─ Header: Phase & Session Info       │
│  ├─ Body: Timer Display & Progress     │
│  └─ Footer: Keybindings & Help         │
├─────────────────────────────────────────┤
│  🧠 Model Layer (State Management)     │
│  ├─ Timer Component (Bubbles)          │
│  ├─ Phase State Machine                │
│  ├─ Session Counter                    │
│  └─ User Preferences                   │
├─────────────────────────────────────────┤
│  ⚡ Update Layer (Event Handling)      │
│  ├─ Timer Tick Messages                │
│  ├─ Keyboard Input                     │
│  ├─ Phase Transitions                  │
│  └─ State Updates                      │
└─────────────────────────────────────────┘
```

## 🚀 Quick Start

### Prerequisites
- **Go 1.21+** installed on your system
- Terminal with Unicode support (recommended)

### Installation

```bash
# Clone the repository
git clone https://github.com/your-username/pomdo.git
cd pomdo

# Install dependencies
go mod tidy

# Build the application
go build -o pomdo

# Run Pomdo
./pomdo
```

### Basic Usage

```bash
# Start a Pomodoro session
./pomdo

# With custom work duration (in minutes)
./pomdo --work 25

# With custom break durations
./pomdo --work 25 --short 5 --long 15
```

## 📋 Implementation Guide

This guide outlines the key steps to build a beautiful terminal-based Pomodoro timer using Go and Bubble Tea. Follow these phases to create a professional CLI application.

### Phase 1: Core Dependencies & Setup

#### 🎨 Install Styling and Layout Libraries

**What you need to do:**
- Install the three main Charm libraries for TUI development
- Set up proper imports in your main Go file
- Understand the role of each library:
  - **Bubble Tea**: The TUI framework for handling events and updates
  - **Bubbles**: Pre-built components like timers, progress bars, and help
  - **Lip Gloss**: Styling framework for colors, borders, and layouts

**Required packages:**
```bash
go get github.com/charmbracelet/lipgloss
go get github.com/charmbracelet/bubbles  
go get github.com/charmbracelet/bubbletea
```

**Key imports to include:**
- Timer component from bubbles
- Help and key components for user interaction
- Progress component for visual feedback
- Core Lip Gloss styling functions

### Phase 2: UI Design & Layout

#### 🖼️ Create Styled Window Panel Layout

**Design your interface structure:**
- **Header section**: Display current phase (Work/Break) with distinctive styling
- **Body section**: Large, prominent timer display in the center
- **Progress section**: Visual progress bar showing completion percentage
- **Footer section**: Help text showing available keyboard shortcuts

**Styling considerations:**
- Use rounded borders for a modern look
- Apply consistent padding and margins throughout
- Create distinct color schemes for different phases
- Ensure text is properly centered and readable
- Make the interface responsive to terminal size changes

**Layout hierarchy:**
- Wrap everything in a main panel with border and padding
- Use vertical layout to stack sections clearly
- Center-align content for professional appearance
- Leave appropriate whitespace between sections

### Phase 3: State Management

#### 🔄 Implement Pomodoro State Machine

**Define your application states:**
- Create an enum or constants for the three phases: Work, Short Break, Long Break
- Track which session number you're currently on
- Count how many complete sessions have been finished
- Store configuration for durations of each phase type

**State transition logic:**
- Start with Work phase and default duration (25 minutes)
- After Work phase, determine if it's time for short break or long break
- Typically use 4 work sessions before triggering a long break
- Reset session counter after long break
- Track total completed sessions for statistics

**Configuration management:**
- Allow customizable durations for work and break periods
- Set sensible defaults (25min work, 5min short break, 15min long break)
- Consider loading settings from config file or command line arguments
- Store user preferences between sessions

### Phase 4: Timer Integration

#### ⏱️ Integrate Bubbles Timer Component

**Timer setup and lifecycle:**
- Initialize timer with current phase duration and 1-second intervals
- Start timer automatically when application launches
- Handle timer tick messages to update the display every second
- Detect when timer reaches zero to trigger phase transitions

**Timer state management:**
- Implement pause/resume functionality
- Allow timer reset to beginning of current phase
- Handle timer updates in your main update loop
- Ensure timer state persists through pause/resume cycles

**Phase transition handling:**
- Detect timer completion events
- Automatically switch to next appropriate phase
- Restart timer with new phase duration
- Update UI to reflect new phase (colors, text, etc.)

### Phase 5: Keyboard Controls & Help

#### ⌨️ Define Keybindings and Help System

**Essential keyboard shortcuts:**
- **Space**: Pause and resume the timer
- **R**: Reset current phase timer to beginning
- **S**: Skip to next phase immediately
- **Q/Ctrl+C**: Quit the application
- **?**: Toggle help display on/off

**Help system implementation:**
- Use Bubbles help component for consistent formatting
- Show short help by default with most important keys
- Allow toggle to full help with detailed descriptions
- Position help text in footer for easy reference
- Update help context based on current application state

**User experience considerations:**
- Make shortcuts intuitive and memorable
- Provide visual feedback when keys are pressed
- Handle edge cases (like pausing during transitions)
- Consider confirmation for destructive actions

### Phase 6: Visual Polish & Animations

#### 🎨 Add Transitions, Animations & Visual Flair

**Phase-based theming:**
- Use warm colors (reds, oranges) for work phases to encourage focus
- Use cool colors (blues, greens) for break phases to promote relaxation
- Apply theme colors to borders, text, and progress bars
- Ensure good contrast and readability in all themes

**Visual feedback and animations:**
- Show progress bar that fills as phase progresses
- Add visual urgency when timer gets low (last 2 minutes)
- Display clear transition messages when phases change
- Consider subtle animations like blinking or color transitions

**Enhanced user experience:**
- Show session progress (e.g., "Session 2/4")
- Display total completed sessions
- Add visual pause indicator when timer is stopped
- Provide clear status information at all times

**System integration:**
- Implement desktop notifications when phases complete
- Add system sound alerts for phase transitions
- Consider integration with system do-not-disturb modes
- Ensure notifications work across different operating systems

## 🎯 Future Enhancements

### Advanced Features
- **📊 Statistics Dashboard**: Weekly/monthly productivity reports
- **🔊 Custom Sounds**: Upload your own notification sounds
- **📝 Task Integration**: Connect with todo lists and project management
- **🌍 Sync Across Devices**: Cloud synchronization of sessions and stats
- **🎵 Focus Music**: Integration with music streaming services
- **📱 Mobile Companion**: React Native app for phone notifications

### Configuration Options
- **⚙️ Custom Durations**: Flexible timer settings per user
- **🎨 Theme System**: Multiple color themes and customization
- **🔧 Hotkey Remapping**: Customizable keyboard shortcuts
- **📈 Goal Setting**: Daily/weekly session targets
- **🏆 Achievement System**: Productivity milestones and rewards

## 🤝 Contributing

We welcome contributions! Here's how to get started:

1. **Fork the repository**
2. **Create a feature branch**: `git checkout -b feat/amazing-feature`
3. **Make your changes** and add tests
4. **Run tests**: `go test ./...`
5. **Commit your changes**: `git commit -m 'Add amazing feature'`
6. **Push to the branch**: `git push origin feat/amazing-feature`
7. **Open a Pull Request**

### Development Guidelines
- Follow Go best practices and conventions
- Write clear, documented code
- Add tests for new functionality
- Update documentation as needed
- Test on multiple terminals and platforms

## 📄 License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.

---

<div align="center">

**Built with ❤️ for productivity enthusiasts**

*Pomodoro Technique © Francesco Cirillo*

[⭐ Star this repo](https://github.com/your-username/pomdo) • [🐛 Report Bug](https://github.com/your-username/pomdo/issues) • [💡 Request Feature](https://github.com/your-username/pomdo/issues)

</div>


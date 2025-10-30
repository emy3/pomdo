# Pomdo

## A CLI based Pomodoro App

### Improvements to Implement

### 1. Install & import styling and layout libraries

Install the libraries:

```
go get github.com/charmbracelet/lipgloss
go get github.com/charmbracelet/bubbles
go get github.com/charmbracelet/bubbletea

Import them in your Go file (for example):
import (
    "github.com/charmbracelet/bubbletea"
    "github.com/charmbracelet/bubbles/timer"
    "github.com/charmbracelet/bubbles/help"
    "github.com/charmbracelet/bubbles/key"
    "github.com/charmbracelet/lipgloss"
)
```

### 2. Create a styled “window” panel layout

Define styles for the panel, header, timer body, footer using Lip Gloss.

In your View() method, create three sections:

Header: e.g., “Pomodoro Timer” + current phase

Body: large timer display

Footer: key hints (e.g., quit, pause, reset)

Wrap those sections inside a styled panel with border and padding so the result looks like a window‑pane.

### 3. Add state machine for Pomodoro phases

Define a type for the phases (Work / Short Break / Long Break).

In your model struct add a field to track the current phase.

On startup, set it to Work with the default work duration (e.g., 25 minutes).

In your Update() method, when timer finishes for one phase, switch to the next phase and set the timer for that phase’s duration (e.g., Work → Short Break → Long Break → back to Work).

Optionally track how many cycles have completed so you know when to trigger a long break.

### 4. Integrate the timer component from Bubbles

Use timer.NewWithInterval(...) (or equivalent) to create a timer with the correct duration and tick interval.

Embed the timer component inside your model struct.

In Init(), start the timer tick command so the countdown begins.

In Update(), handle timer tick messages (timer.TickMsg or similar) and update the timer state.

When the timer indicates it’s done, trigger your phase‑switch logic.

### 5. Define keybindings and help view

Use the key package to define bindings for actions: e.g., pause/resume, reset, quit.

Use the help package to render a help view which shows the keys and their actions.

In your View(), include the help view in the footer section so the user sees what keys are available.

### 6. Add transitions / flair

Change colours/styles based on phase. For example:

Work phase: header or timer in red/orange

Break phase: green/blue

Optionally add a progress bar (with Bubbles’ progress component) to show how far through the phase you are.

Possibly add a short animation or visual cue when phase changes (e.g., flash, message “Time for a break!”).

Use Lip Gloss styling (padding, margins, colour backgrounds) to make things visually pleasing.

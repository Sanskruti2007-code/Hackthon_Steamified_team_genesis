# Virtual_CRO

## Problem Statement Fit

Virtual_CRO is a browser-based immersive virtual laboratory designed for the Hackathon-YCCE-September-2026 problem statement **“Familiarisation with Oscilloscope and Function Generator.”**

The solution addresses the difficulty students face while learning practical CRO operation, waveform measurement, triggering, scaling, probe connection, and troubleshooting on physical laboratory equipment.

Instead of a static 2D simulator, the project is designed as an interactive 3D electronics laboratory where students can operate a virtual Cathode Ray Oscilloscope (CRO) and Function Generator, observe real-time waveform changes, manually measure signals using the graticule, and troubleshoot controlled faults in a safe environment.

> **Core Idea:** An immersive 3D virtual CRO laboratory that combines realistic instrument operation with AI-guided learning and controlled fault injection, enabling students to practice both waveform measurement and real-world troubleshooting in a risk-free environment.

## Target Users

The primary users are:
- Engineering students learning Analog Electronics and CRO operation
- Students preparing for electronics laboratory practicals
- Faculty demonstrating oscilloscope concepts
- Peer learners using guided/spectator sessions
- Hackathon judges evaluating an educational simulation

The main learning problems addressed are:
- Difficulty understanding CRO front-panel controls
- Lack of practical experience with Volts/Div and Time/Div
- Difficulty stabilizing a waveform using trigger controls
- Difficulty manually reading waveform parameters from a graticule
- Fear of making incorrect hardware connections
- Limited access to physical laboratory instruments
- Lack of realistic troubleshooting practice

## What We Are Building

We are building a lightweight, deployment-ready web simulation using HTML, CSS and JavaScript with a 3D laboratory environment.

The application is structured into modular components for:
- 3D electronics lab environment
- CRO instrument interaction
- Function generator interaction
- BNC probe connection
- Signal generation and mathematical waveform modelling
- CRO display and 8×10 graticule
- Triggering and positioning
- Dual-channel operation
- X-Y / Lissajous visualization
- Manual waveform measurement
- Controlled fault injection
- AI-guided learning
- Assessment and performance tracking

The initial project scaffold is created through **CreatorCode** and is being developed incrementally feature-by-feature so that each subsystem can be tested, validated and committed separately.

## Core Features

### 1. 3D Instrumentation Workbench

The virtual workbench contains:
- Cathode Ray Oscilloscope
- Function Generator
- BNC probes/cables
- Interactive camera view
- Instrument controls and status indicators

### 2. CRO Control Panel

The CRO provides interactive controls for:
- Power
- Channel 1 / Channel 2
- Volts/Division
- Time/Division
- Vertical position
- Horizontal position
- Trigger level
- Trigger source
- Trigger mode
- AC / DC / GND coupling
- Focus
- Intensity
- X-Y mode

Every control is intended to produce a visible effect on the simulated instrument.

### 3. Function Generator

The Function Generator supports:
- Sine wave
- Square wave
- Triangle wave
- Frequency control
- Amplitude control
- DC offset
- Output enable
- Channel routing
- Optional phase control

### 4. Dual-Channel Signal Flow

Two independent signal paths are supported:

```text
Function Generator
       |
       v
    BNC Cable
       |
   +---+---+
   |       |
  CH1     CH2
   |       |
   +---+---+
       |
       v
   CRO Display
```

A disconnected or incorrect BNC path prevents the corresponding signal from appearing on the CRO.

### 5. Procedural Waveform Display

The CRO display dynamically renders:
- Sine
- Square
- Triangle

The waveform responds to:
- Frequency
- Amplitude
- DC offset
- Volts/Div
- Time/Div
- Position
- Trigger settings
- Coupling mode

### 6. Functional 8×10 Graticule

The CRO screen contains an 8×10 measurement grid.

Students manually determine:
- Peak-to-peak voltage
- Amplitude
- Time period
- Frequency
- Optional phase difference

The project intentionally preserves the manual measurement workflow instead of automatically revealing the answer.

### 7. Triggering and Positioning

Students can:
- Set trigger level
- Select trigger source
- Adjust horizontal position
- Adjust vertical position
- Stabilize the displayed waveform

### 8. X-Y Mode

The X-Y mode uses:
- CH1 as the X-axis signal
- CH2 as the Y-axis signal

This enables Lissajous-pattern experiments for frequency comparison and phase relationships.

### 9. Controlled Fault Injection

Fault scenarios simulate realistic beginner troubleshooting cases, including:
- BNC probe disconnected
- Function generator output disabled
- Wrong channel selected
- Incorrect trigger source
- Incorrect trigger level
- Incorrect Time/Div
- Incorrect Volts/Div
- GND coupling
- Excessive DC offset
- Optional noisy/distorted signal

The system can expose a symptom first and require the student to identify the cause.

### 10. AI Instructor

The AI Instructor is a learning assistant that can:
- Explain CRO controls
- Give progressive hints
- Ask diagnostic questions
- Explain why a waveform is missing or unstable
- Guide manual measurement
- Explain faults after an attempt
- Summarize the student's mistakes
- Suggest the next learning exercise

During assessment mode, the AI is designed to guide reasoning rather than directly giving the final answer before the student's attempt.

### 11. Assessment and Performance

The application can track:
- Scenario
- Instrument settings
- Student measurement
- Attempts
- Hint usage
- Time taken
- Fault diagnosed
- Final result

A session summary can show:
- Accuracy
- Attempts
- Completion time
- Topics needing more practice

### 12. Spectator / Review Mode

An advanced mode can allow another user to observe:
- CRO settings
- Waveform
- Graticule
- Measurement state
- Fault state
- Session progress

For the MVP, this can be implemented as a read-only shared session state before expanding to full real-time multi-user interaction.

## Technical Architecture

```text
                    3D LAB UI
                       |
        +--------------+--------------+
        |              |              |
        v              v              v
 Function         CRO Controller   BNC / Connection
 Generator             |              |
        +--------------+--------------+
                       |
                       v
              Signal Engine
                       |
                Trigger Engine
                       |
                       v
              CRO Display Engine
                 8 × 10 Grid
                       |
                       v
              Manual Measurement
                       |
             +---------+---------+
             |                   |
             v                   v
       Fault Engine         AI Instructor
             |                   |
             +---------+---------+
                       |
                       v
              Assessment / Data
```

## Mathematical Model

For a sinusoidal signal:

```text
V(t) = Voffset + A sin(2πft + φ)
```

Where:
- `A` = peak amplitude
- `Vpp` = peak-to-peak voltage
- `f` = frequency
- `φ` = phase

### Voltage measurement

```text
Vpp = vertical_divisions × VoltsPerDivision
A = Vpp / 2
```

### Time / frequency measurement

```text
T = horizontal_divisions × TimePerDivision
f = 1 / T
```

### Phase measurement

```text
Phase = (Δt / T) × 360°
```

The renderer uses these relationships to translate mathematical signal parameters into the virtual CRO display.

## Tech Stack

### Frontend / 3D
- HTML5
- CSS3
- JavaScript (ES Modules)
- Three.js for browser-based 3D rendering
- Canvas / Three.js rendering for dynamic waveform visualization

### Backend / Data
- Supabase PostgreSQL for session, scenario and assessment data
- Supabase Auth if authentication is required
- Supabase Realtime for shared/spectator session state
- Secure server-side function/API layer for AI calls

### AI
- Approved LLM/API provider selected according to hackathon availability
- AI requests routed through a secure backend/API layer
- API keys must never be hardcoded into frontend JavaScript

### Version Control and Deployment
- Git
- GitHub
- CreatorCode validation
- Deployment configuration supplied by the hackathon workflow

> **Dependency rule:** approved packages/assets should be installed through the CreatorCode workflow rather than adding random unapproved dependencies manually.

## Innovation / Uniqueness

The project combines four elements in one learning environment:

1. **Realistic instrument interaction**  
   Students learn where controls are and how those controls affect the displayed waveform.

2. **Procedural mathematical simulation**  
   The waveform is generated from signal parameters instead of using a static screenshot or pre-recorded animation.

3. **Controlled troubleshooting**  
   Students can intentionally encounter realistic faults and diagnose them without risking real hardware.

4. **AI-guided learning**  
   An instructor-style AI layer provides hints and explanations while keeping the student responsible for the manual measurement and troubleshooting task.

This turns the simulation from a simple waveform viewer into a practical learning and troubleshooting environment.

## Final User Journey

1. Student enters the virtual electronics laboratory.
2. CRO and Function Generator are initially powered off.
3. Student powers on both instruments.
4. Student picks up and connects the BNC probe.
5. The system validates the connection.
6. Student chooses a waveform on the Function Generator.
7. Student sets frequency and amplitude.
8. Signal appears on CRO Channel 1 or Channel 2.
9. Student adjusts Time/Div and Trigger controls until the waveform is stable.
10. Student adjusts Volts/Div and position.
11. Student manually counts the graticule divisions.
12. Student calculates Vpp and frequency.
13. Student submits the values in the virtual measurement notebook.
14. System evaluates the attempt.
15. AI provides targeted feedback or a progressive hint.
16. A controlled fault is introduced.
17. Student diagnoses and corrects the fault.
18. The session ends with an assessment and learning summary.

## Demo Scenario

### Mystery Sine Wave

The student receives a signal whose actual values are not displayed directly.

The student must:
1. Connect Channel 1.
2. Configure the Function Generator.
3. Stabilize the waveform.
4. Set appropriate Volts/Div.
5. Set appropriate Time/Div.
6. Count vertical divisions.
7. Count horizontal divisions.
8. Calculate Vpp.
9. Calculate frequency.
10. Submit the readings.

After the measurement task, a controlled fault such as **Trigger Level Mismatch** or **BNC Disconnection** is injected.

The student must observe the symptom, reason about the cause, and restore the CRO to a usable state.

## MVP

### Must Have
- 3D lab scene
- CRO
- Function Generator
- BNC connection logic
- CH1 and CH2
- Sine / Square / Triangle waveforms
- Volts/Div
- Time/Div
- 8×10 graticule
- Trigger control
- Manual voltage/frequency measurement
- X-Y mode
- At least one controlled fault
- AI hint interface
- Assessment result
- GitHub repository with meaningful commits

### Advanced
- Realistic CRT focus/intensity behaviour
- Larger fault library
- Adaptive AI tutoring
- Full spectator synchronization
- Session replay
- Instructor dashboard
- Advanced probe physics
- Advanced phase experiments
- Additional lab scenarios

## Repository / Development Workflow

The project is being built incrementally with small, understandable commits.

Recommended sequence:

```text
initial project setup
add base lab scene
add CRO instrument
add function generator
add BNC connection
add signal engine
add trigger engine
add 8x10 graticule
add manual measurement
add dual channel
add X-Y mode
add fault injection
add AI instructor
add assessment flow
integrate backend
integrate final demo
fix creatorcode validation
```

Each feature should be tested before the next feature is integrated.

## Current Project Status

The repository currently contains the CreatorCode-generated baseline and project configuration. The functional simulation is being implemented incrementally.

Current baseline includes:
- HTML/CSS/JavaScript project scaffold
- Vite development workflow
- Deployment configuration
- CreatorCode project metadata
- Submission documentation

Upcoming implementation work will add the simulation modules described above.

## Known Limitations of the Current Baseline

- The complete 3D laboratory is not yet implemented.
- The backend/database is not yet connected.
- AI integration is not yet connected.
- Fault scenarios are not yet fully implemented.
- Full multi-user spectator mode is an advanced milestone.
- Final 3D models and interaction physics are still under development.

## Future Work

- Complete the interactive 3D electronics laboratory.
- Add realistic CRO and Function Generator models.
- Implement complete mathematical waveform and trigger engines.
- Connect Supabase for persistent learning data.
- Add secure AI Instructor integration.
- Expand fault-injection scenarios.
- Add spectator/review functionality.
- Improve CRT visual realism and performance.
- Add more learning and assessment scenarios.

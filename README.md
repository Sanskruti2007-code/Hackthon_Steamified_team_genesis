# Virtual_CRO

### Hackathon-YCCE-September-2026
**Familiarisation with Oscilloscope and Function Generator**

> An immersive 3D virtual CRO laboratory with realistic instrument operation, AI-guided learning and controlled fault injection.

## Problem

Students often learn CRO theory without enough practical experience with:

- Volts/Div and Time/Div
- Triggering and waveform stabilization
- Probe/BNC connections
- Manual graticule measurement
- Dual-channel and X-Y operation
- Troubleshooting incorrect settings

## Solution

Virtual_CRO creates a browser-based 3D electronics laboratory where students can operate a virtual CRO and Function Generator, observe real-time waveforms, manually measure signals and troubleshoot faults safely.

## Key Features

- 3D electronics workbench
- Virtual CRO and Function Generator
- BNC probe connection
- CH1 and CH2
- Sine, Square and Triangle signals
- Volts/Div and Time/Div
- Trigger and positioning controls
- AC/DC/GND coupling
- 8×10 graticule
- Manual Vpp and frequency measurement
- X-Y / Lissajous mode
- Controlled fault injection
- AI Instructor
- Assessment and session summary
- Future spectator/review mode

## Signal Flow

```text
Function Generator
      ↓
   BNC Probe
      ↓
    CH1/CH2
      ↓
 Signal Engine
      ↓
Trigger + Scaling
      ↓
 CRO Display
      ↓
Manual Measurement
      ↓
Assessment + AI Feedback
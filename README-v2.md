# SCP: Echoes of the Void

```text
========================================================================================
                      SITE-19 SUB-LEVEL SECURITY & COMMAND SYSTEM
========================================================================================
           SCP: ECHOES OF THE VOID -- TACTICAL TERMINAL COMMAND INTERFACE
========================================================================================
```

**Genre**: Tactical Management / Remote Containment Simulator  
**Interface Aesthetic**: Retro Desktop Operating System / Faux-TUI  
**Core Paradigm**: Indirect Telemetry & Command-Line Operations  
**Design Purpose**: System Design Guideline & Project Architecture  

---

## Overview

**SCP: Echoes of the Void** is a tactical, terminal-oriented management game set within the SCP Foundation universe. Operating from inside a locked site control room following a catastrophic containment breach, the player uses a retro desktop environment, an ncurses-style vector map, and a command-line interface (CLI) to guide surviving staff to safety, command Mobile Task Force (MTF) fireteams, and re-contain dangerous anomalous entities.

The game eliminates direct visual camera feeds, forcing the player to make critical decisions based on indirect sensory telemetry, room occupancy counters, motion triplines, and environmental logs.

---

## Table of Contents

1. [Project Narrative & Premise](#project-narrative--premise)
2. [Gameplay Progression: The Four Tiers](#gameplay-progression-the-four-tiers)
3. [Desktop Interface & Shell Layout (Faux-TUI)](#desktop-interface--shell-layout-faux-tui)
4. [Virtual Windowing System Architecture](#virtual-windowing-system-architecture)
5. [Sensory Deduction & Vector Telemetry Engine](#sensory-deduction--vector-telemetry-engine)
6. [Factions & Entity Behaviors](#factions--entity-behaviors)
7. [MTF Command, Modular Doctrines & Physical Logistics](#mtf-command-modular-doctrines--physical-logistics)
8. [System Architecture & Data Flow Diagram](#system-architecture--data-flow-diagram)

---

## Project Narrative & Premise

* **Setting & Protagonist**: You play as a junior systems administrator undergoing training at Site-19 when a site-wide containment breach occurs. With your supervisor killed during the initial chaos, you are left alone inside the fortified Control Room.
* **Interface**: The entire game takes place on your terminal monitor through a custom retro operating system mimicking a modernized Windows 98 desktop interface.
* **Core Loop**: Without live video camera feeds or 3D character models, you monitor the facility indirectly using room occupancy counters, motion triplines, and environmental telemetry. You issue commands via CLI (`WIN_TERM`) and coordinate survival routes across an ASCII/vector schematic (`WIN_MAP`).

---

## Gameplay Progression: The Four Tiers

The game unfolds across four escalating operational phases:

```text
+------------------------------------------------------------------------------------+
| TIER 1: PRE-BREACH (TUTORIAL)                                                      |
| Follow orders from senior sysadmin; learn basic terminal syntax & door controls.   |
+------------------------------------------------------------------------------------+
                                         | (Containment Breach Occurs)
                                         v
+------------------------------------------------------------------------------------+
| TIER 2: TRIAGE & EVACUATION                                                        |
| Guide surviving scientists & guards to safezone bunkers. Initiate MTF distress call.|
+------------------------------------------------------------------------------------+
                                         | (Reinforcement Timer Expires)
                                         v
+------------------------------------------------------------------------------------+
| TIER 3: TACTICAL CONTAINMENT (CORE GAMEPLAY)                                       |
| MTF fireteams arrive. Deploy specialized units, re-contain anomalies, clear routes. |
+------------------------------------------------------------------------------------+
                                         | (All Personnel Tokens Depleted)
                                         v
+------------------------------------------------------------------------------------+
| TIER 4: RESOLUTION (THE LAST CALL)                                                 |
| Deploy MTF Alpha-1 with master override keycards to initiate Warhead protocol.     |
| Single attempt -- if Alpha-1 perishes, GAME OVER.                                  |
+------------------------------------------------------------------------------------+
```

1. **Tier 1: Pre-Breach (Tutorial)**: A brief onboarding section following routine instructions from your supervisor before containment fails.
2. **Tier 2: Triage & Evacuation**: Fast-paced survival phase. You have restricted low-level authorization. Your objective is to route staff into safehouses (saving staff grants future system upgrades and reduces hostile conversions) and initiate an emergency call to HQ to start the MTF arrival countdown.
3. **Tier 3: Tactical Containment**: Primary gameplay loop. MTF reinforcements arrive. You dispatch fireteams via `WIN_DISPATCH`, command them via CLI, and navigate containment sectors.
4. **Tier 4: Resolution (The Last Call)**: Triggered if all standard MTF tokens are exhausted. MTF Alpha-1 arrives with master override keycards to manually calibrate and initiate the site's Warhead failsafe protocol (e.g., thermal rod realignment). If Alpha-1 perishes, the session ends in failure.

---

## Desktop Interface & Shell Layout (Faux-TUI)

The UI is styled after a retro operating system desktop environment, utilizing 3D beveled panel borders, navy blue active title bars, dark slate/teal wallpaper, and a functional bottom taskbar.

### ASCII Desktop UI Layout
```text
+------------------------------------------------------------------------------------+
| [ WIN_DESKTOP: Modernized Windows 98 Shell / Faux-TUI Frame ]                      |
| +-----------------------------------------+ +------------------------------------+ |
| | +-[ WIN_MAP ]------------------[_][^][X]| | +-[ WIN_TERM ]-------------[_][^][X]| |
| | | [G] Open  [Y] Closed  [R] Locked/Err | | | > scan CORRIDOR-04              | |
| | | [!] Noise Spike   [?] Ambiguous Move | | |   MASS: UNKNOWN (RAPID VELOCITY)| |
| | | Occupancy Headcounts / Triplines     | | | > door DOOR-08 lock             | |
| | +--------------------------------------+ | +----------------------------------+ |
| | +-[ WIN_LOG ]------------------[_][^][X]| | +-[ WIN_DISPATCH ]---------[_][^][X]| |
| | | 13:02:11 DOOR-04 ACTUATOR CRITICAL   | | | RESERVE: [----====] 04/08 TOKENS | |
| | | 13:02:14 SENSOR DEVIATION SEC-02     | | | DOCTRINE: [ BETA-7 (HAZMAT) ]    | |
| | +--------------------------------------+ | +----------------------------------+ |
| +----------------------------------------------------------------------------------+ |
| | [START] | [WIN_MAP] | [WIN_TERM] | [WIN_LOG] | [WIN_DISPATCH]       13:02:15     | |
| +----------------------------------------------------------------------------------+ |
+------------------------------------------------------------------------------------+
```

### Core Application Windows
* **WIN_TERM**: Command-Line Interface for queries (`scan`, `ping`, `diag`) and environmental control (`door`, `lockdown`, `bunker`).
* **WIN_MAP**: Interactive vector schematic displaying room boundaries, door status tokens, and motion triplines.
* **WIN_LOG**: Real-time telemetry feed recording actuator stress warnings, power breaker trips, and environmental deviations.
* **WIN_DISPATCH**: Curses-style requisition terminal used to assemble MTF fireteams, assign doctrines, and equip physical site depot inventory.

---

## Virtual Windowing System Architecture

The desktop operates as an abstract window management environment. To ensure a retro operating system feel, the windowing framework follows key UI structural guidelines:

### Window Shell & Structural Guidelines
* **Title Bar Frame**: Every active application window features a dedicated title bar containing the app icon, title text, and control buttons (Minimize `_`, Maximize/Restore `^`, Close `X`).
* **Draggable Canvas**: Clicking and dragging a window's title bar relocates its position on the desktop grid.
* **8-Way Edge Resizing**: Windows detect mouse hover along an 8-pixel border perimeter (North, South, East, West, and 4 corners), allowing dynamic scaling with strict minimum width/height thresholds.
* **Focus & Z-Ordering**: Clicking anywhere within a window raises its visual layer to the top of the stack and highlights its title bar with active color styling.
* **Taskbar Integration**: Minimizing a window hides its viewport while keeping an active button on the bottom taskbar, allowing instant toggle restoration.

---

## Sensory Deduction & Vector Telemetry Engine

Information in the control room is split across two operational layers:

### Layer 1: Passive Vector Map Telemetry
* **Door Status Tokens**:
  * `[G]` **Green**: Open / Unlocked.
  * `[Y]` **Yellow**: Closed (Standard state; keycards required for personnel passage).
  * `[R]` **Red**: Locked or Mechanical Error / Jammed.
* **Room Node & Corridor Flags**:
  * `[!]`: Critical Alert (Decibel spike, pressure shift, or door breach attempt).
  * `[?]`: Ambiguous Contact (Unregistered transponder motion detected).
  * `[#]`: Verified Friendly Transponder Ping.
  * **Occupancy Counters**: Displays floor pressure plate counts (`OCCUPANCY: 02`).

### Layer 2: Active CLI Commands & Query Pipeline
Commands take time to execute (locking the CLI buffer for 2-3 seconds) to create operational friction:

| Command Group | Syntax | Functional Objective | Operational Constraint / Risk |
| :--- | :--- | :--- | :--- |
| **Telemetry** | `scan [room/zone]` | Runs thermal & biometric mass checks | 2-3 second execution delay |
| **Telemetry** | `ping [zone/id]` | Queries Foundation transponder badges | Fails to detect SCPs or Class-D |
| **Telemetry** | `diag [door_id]` | Returns actuator stress & heat levels | Informational only; does not repair |
| **Control** | `door [id] [open/lock]` | Toggles door state | Builds actuator heat & consumes power |
| **Control** | `lockdown [zone]` | Emergency seals an entire wing | Traps friendlies; high electrical draw |
| **Control** | `bunker [id] [seal]` | Operates heavy safezone blast doors | Slow 5-8s hydraulic cycle time |

### Door Constraints & Mechanical Failures
1. **Actuator Stress & Burnout**: Keeping a door forced shut (`[R]`) causes thermal stress buildup. Banging anomalies accelerate wear until the motor burns out, leaving the doorway permanently jammed open or closed.
2. **Breaker Power Caps**: The control room power supply limits the number of active magnetic locks. Sealing one hallway requires unsealing another.
3. **Hydraulic Cycles**: Heavy blast doors cycle slowly, leaving evacuees vulnerable if timing is miscalculated.

---

## Factions & Entity Behaviors

| Faction | Transponder Signal | Tactical Behavior & Role |
| :--- | :--- | :--- |
| **Scientists & Staff** | Active Badge | Panicky non-combatants; granting shelter yields system upgrades |
| **Security Guards** | Active Badge | Early defenders; finite ammo; escort capability |
| **Class-D Personnel** | Unregistered | Opportunists; may assist or sabotage facility systems |
| **Chaos Insurgency** | Hostile Signal | Armed infiltrators; inject malicious CLI code into terminal |
| **Mobile Task Forces** | Friendly Tactical | Player-commanded tactical fireteams with specialized doctrines |
| **Anomalies (SCPs)** | None / Anomalous | Governed by canonical anomaly behaviors and sensory triggers |

---

## MTF Command, Modular Doctrines & Physical Logistics

### Curses-Style Requisition Interface (`MTF_CONFIG.EXE`)
```text
+-[ MTF REQUISITION: ARMORY LOCKER 01 ]------------------------[_][^][X]-+
| ACTIVE PERSONNEL TOKENS: [----====] 08/12 REMAINING                 |
+--------------------------------------------------------------------+
| [1] SQUAD TYPE (DOCTRINE)                                          |
|     ( ) MTF E-11  "Nine-Tailed Fox"   [Tactical / Ballistics]      |
|     (*) MTF B-7   "Maz Hatters"       [Hazmat / Biohazard]         |
|     ( ) MTF H-10  "See No Evil"       [Cognito / Visual Filter]    |
|     ( ) MTF Z-9   "Mole Rats"         [Structural / Lidar]         |
|                                                                    |
| [2] TEAM COMPOSITION                                               |
|     [ - ]  [ 04 OPERATORS ]  [ + ]     (-4 Personnel Tokens)       |
|                                                                    |
| [3] PHYSICAL WEAPON LOCKER (CHOOSE 1 PER SQUAD)                    |
|     ( ) FN P90 SMG              [ IN STOCK: 02 ]                   |
|     (*) LV-4 NEURO-DISPERSER    [ IN STOCK: 01 ] (LAST UNIT)       |
|     ( ) CR-1 CRYOPROJECTOR      [ IN STOCK: 00 ] (LOCATED: LAB-04) |
|                                                                    |
| [4] TACTICAL PAYLOAD                                               |
|     (*) HYDRAULIC SPREADER      [ IN STOCK: 01 ]                   |
|     ( ) REALITY ANCHOR (SRA)    [ IN STOCK: 00 ] (LOCKED: SEC-03)  |
|                                                                    |
| [5] INSERTION POINT: [ CARGO ELEVATOR 02 ]                         |
+--------------------------------------------------------------------+
| [TAB] Cycle Section  |  [UP/DOWN] Select  |  [ENTER] Authorize     |
+--------------------------------------------------------------------+
```

### Tactical Task Force Matrix
| Task Force | Specialization | Strengths (Dominates) | Critical Blindspot |
| :--- | :--- | :--- | :--- |
| **Epsilon-11 (E-11)** | Nine-Tailed Fox / Heavy Ballistics | Armed Class-D, CI, Physical Brutes | Airborne Biohazards (Spores infect operators) |
| **Beta-7 (B-7)** | Maz Hatters / Hazmat & Bio-Seals | Viral blooms, toxins, chemical leaks | Kinetic / Slashing Threats (Suits rupture easily) |
| **Eta-10 (H-10)** | See No Evil / SCRAMBLE Visors | Visual Cognitohazards, gaze triggers | Acoustic / Stealth Threats (Feed latency) |
| **Zeta-9 (Z-9)** | Mole Rats / Structural & Lidar | Non-Euclidean geometry, jammed `[R]` doors | Open Firefights (Slow traversal speed) |

### Physical Depot Logistics & Scavenging
* **No Abstract Points**: Equipment is managed as tangible physical inventory.
* **Armory Infiltration**: High-tier counters (Cryoprojectors, Scranton Reality Anchors) are locked inside facility armories. Players must guide squads or guards to unlock lockers and stage equipment.
* **Field Stripping**: When an MTF fireteam perishes, their equipped gear remains on their bodies. Subsequent squads must be routed to the death site to recover dropped equipment.

---

## System Architecture & Data Flow Diagram

```text
========================================================================================
                      SITE-19 SYSTEM ARCHITECTURE & DATA FLOW
========================================================================================

 [ WIN_DESKTOP: Modernized Windows 98 Shell / Faux-TUI Frame ]
 +------------------------------------------------------------------------------------+
 | +-[ WIN_MAP ]------------------[_][^][X]+  +-[ WIN_TERM ]------------------[_][^][X]+ |
 | | [G] Open  [Y] Closed  [R] Locked/Err  |  | > scan CORRIDOR-04                    | |
 | | [!] Noise Spike   [?] Ambiguous Move  |  |   MASS: UNKNOWN (RAPID VELOCITY)      | |
 | | Occupancy Headcounts / Triplines      |  | > door DOOR-08 lock                   | |
 | +---------------------------------------+  +---------------------------------------+ |
 | +-[ WIN_LOG ]------------------[_][^][X]+  +-[ WIN_DISPATCH ]--------------[_][^][X]+ |
 | | 13:02:11 DOOR-04 ACTUATOR CRITICAL    |  | RESERVE: [----====] 04/08 TOKENS      | |
 | | 13:02:14 SENSOR DEVIATION SEC-02      |  | DOCTRINE: [ BETA-7 (HAZMAT) ]         | |
 | +---------------------------------------+  +---------------------------------------+ |
 | [START] | [WIN_MAP] | [WIN_TERM] | [WIN_LOG] | [WIN_DISPATCH]       13:02:15       |
 +------------------------------------------------------------------------------------+
                                      |
       +------------------------------+-------------------------------+
       |                                                              |
       v                                                              v
 [ PHASE 1: TRIAGE & SURVIVAL ]                     [ PHASE 2: TACTICAL RE-CONTAINMENT ]
 (Junior Tech Alone in Control Room)                 (MTF Fireteams Inbound)
       |                                                              |
       +---> SENSOR RECON LOOP                                        +---> REQUISITION & ASSEMBLY
       |     * Passive Vectors (Map blips, decibels)                  |     * Strict finite token pool
       |     * Active CLI (scan, ping, diag)                          |     * Physical depot items
       |     * Deduce Civilians vs Anomalies                          |     * Scavenge lockers / dead squads
       |                                                              |
       +---> DOOR & HAZARD CONTROL                                    +---> TACTICAL ATTRITION LOOP
       |     * Cycle bulkheads ([G] / [Y] / [R])                      |     * Rock-Paper-Scissors matchups:
       |     * Actuator stress & motor burnout                        |       - E-11: Brute / Ballistic
       |     * Breaker limits & cycle delays                          |       - B-7:  Bio / Contagion
       |                                                              |       - H-10: Visual / Cognito
       v                                                              v
 [ GOAL: Route Staff to Safe Bunkers ]              [ CONSEQUENCE: Fallen MTF Turn to Hazards ]
```
## Technologies used
  Engine - GODOT
  Audio design - Audacity
  AI is used only for idea agregation and design unity
---

*Grounded in SCP Foundation lore. Designed as a high-level system architectural specification.*

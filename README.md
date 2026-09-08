<p align="center">
  <img src="SCADAScop-AnimatedSplashScreen.gif" alt="SCADAScop" width="900">
</p>

**SCADAScop** is a free **multiprotocol SCADA testing tool** with a modern,
dockable **Dear ImGui** interface. It brings the whole Scop family into one
application: **Modbus**, **DNP3 (IEEE 1815)**, **IEC 60870-5-104**, and
**IEC 60870-5-101** — each as **Master and Slave** — all running **at the same
time** on one grouped channel tree. Poll real PLCs over Modbus while simulating a
DNP3 outstation and an IEC 104 station for the SCADA under test, in a single
window, with one workspace file.

Every protocol stack is **hand-rolled over Asio**, with no third-party protocol
library, and shared with the standalone ModbusScop, DNPScop, IEC104Scop, and
IEC101Scop tools.

Free to use and redistribute under the permissive **BSD 2-Clause License**.

Developed by **Carlos Nardi**.

[![Buy Me A Coffee](https://img.shields.io/badge/Buy%20Me%20A%20Coffee-support-yellow?logo=buy-me-a-coffee)](https://buymeacoffee.com/cnardi)

<p align="center">
  <img src="SCADAScop Window 1.0.png" alt="SCADAScop" width="1200">
</p>

## Concept

SCADAScop is organized as a tree: **Groups → Channels → (protocol-native
subtree)**.

- A **Group** is a user-named container — a substation, a bay, a test rig. Use
  one or many; the tree stays flat while there is only one.
- A **Channel** declares a **Role** (Master or Slave) and a **Protocol** (Modbus,
  DNP3, IEC 60870-5-104, IEC 60870-5-101), then the matching Scop tool's own New
  Channel dialog asks for the endpoint: TCP, UDP, or serial, as each protocol
  allows. Each channel runs on its own I/O thread and **keeps running regardless
  of what is on screen**; start and stop them independently. Every channel has
  an **accent color** (a per-protocol default, or your own) that also tints that
  channel's windows.
- Under each channel the tree shows the **protocol-native structure** you know
  from the standalone tools — RTUs and maps for Modbus, outstations and points for
  DNP3, stations and information objects for IEC — with the same context menus
  (Add RTU, Points, Events, Messages, Tools…) and the same working windows.

## Included tools

| Protocol | Master | Slave |
|----------|--------|-------|
| Modbus TCP / UDP / RTU (serial, and RTU over the network) | ModbusScop Master | ModbusScop Slave |
| DNP3 (IEEE 1815) over TCP / UDP / serial | DNPScop Master | DNPScop Slave |
| IEC 60870-5-104 over TCP | IEC104Scop Master | IEC104Scop Slave |
| IEC 60870-5-101 over serial / TCP tunnel | IEC101Scop Master | IEC101Scop Slave |

Each tool is the same code as its standalone release — poll windows, point
databases, message schedules, simulation, glue logic, fault injection, CSV
import/export, and the per-protocol Communication Monitor with layered frame
decode are all there. See the individual tool READMEs for the full protocol
feature lists.

## Features

- **All eight tools at once** — any mix of protocols and roles, hosted in one
  docking space, one menu bar, one status bar. Tools are instantiated on demand
  the first time a channel of that kind is created.
- **Grouped channel tree** — organize channels into named groups, reorder them,
  move channels between groups, and color-code each channel. The tree blinks on
  traffic per channel.
- **One Status Messages window** — the merged, timestamped stream of every
  tool's events, colored by protocol, with a *Source* column.
- **One Dashboard** — a collapsible section per protocol tool with its live
  traffic counters and connection state.
- **Per-protocol windows on demand** — each tool's own windows (Live Data Map,
  Communication Monitor, Events, Points, Messages, poll windows…) are one click
  away under **View → *tool name***.
- **One workspace** — **File → Save Workspace** writes a single `.ssw` file that
  records groups, channel bindings, and accent colors, alongside one native
  workspace side file per protocol tool, so every channel, point, schedule, and
  simulation is restored together. SCADAScop **reopens the last workspace on
  launch** and keeps a recent-files list.
- **One look** — dark / light / classic themes with a customizable accent color,
  DPI scaling, always-on-top, GPU or CPU rendering; the shell owns the theme so
  every tool matches.
- **Animated splash and About** — the family's animated splash rotates its style
  on each launch.

## Download & run

1. Go to the [**Releases**](../../releases) page and download the latest
   `SCADAScop` archive for Windows.
2. Unzip it anywhere and run **`SCADAScop.exe`** — no installation required.

**Requirements:** Windows 10/11 (64-bit).

**Rendering:** SCADAScop uses the GPU by default; you can switch to **CPU
(software)** rendering under **View → Rendering** (handy over Remote Desktop or in
VMs).

### Getting started

1. **Channel → New Channel...** (Ctrl+N) or **+ Channel** — pick the **Role**
   (Master / Slave) and the **Protocol**, press **Continue**, and fill in that
   tool's endpoint dialog (host and port, bind address, COM port, link addresses,
   framing…).
2. Repeat for every device you want to poll or simulate — a Modbus master
   channel to a PLC, a DNP3 slave channel for the SCADA, an IEC 104 station…
   Optionally **+ Group** to organize them and pick an **Accent color** per
   channel.
3. Expand a channel to work with its RTUs, points, maps, and schedules exactly
   as in the standalone tool; right-click for the tool's own actions.
4. Press **Start** on each channel. Follow everything in the shared **Status
   Messages** and **Dashboard**, and open a protocol's **Communication Monitor**
   from the **View** menu to see its frames decoded.

Use **File → Save Workspace** (Ctrl+S) to keep the whole multiprotocol setup and
reload it later with **Open Workspace** (Ctrl+O) — or just start SCADAScop again;
it reopens the last workspace.

## Third-party libraries

SCADAScop is built with these open-source components, each under its own license:

| Library | Used for | License |
|---------|----------|---------|
| Dear ImGui (docking) | user interface | MIT |
| GLFW 3 | window / OpenGL context | Zlib/libpng |
| OpenGL 3 | rendering | — |
| Asio (standalone) | TCP / UDP / serial transport for every protocol | Boost Software License 1.0 |
| stb_image | logo / splash decoding | MIT / public domain |

The Modbus, DNP3, IEC 60870-5-104, and IEC 60870-5-101 protocol stacks are
original code, not third-party libraries.

## License

SCADAScop is released under the **BSD 2-Clause License**. It is provided "as is",
without warranty of any kind; the author is not responsible for any damage or
loss caused by its use.

```
BSD 2-Clause License

Copyright (c) 2026, Carlos Nardi
All rights reserved.

Redistribution and use in source and binary forms, with or without
modification, are permitted provided that the following conditions are met:

1. Redistributions of source code must retain the above copyright notice,
   this list of conditions and the following disclaimer.

2. Redistributions in binary form must reproduce the above copyright notice,
   this list of conditions and the following disclaimer in the documentation
   and/or other materials provided with the distribution.

THIS SOFTWARE IS PROVIDED BY THE COPYRIGHT HOLDERS AND CONTRIBUTORS "AS IS"
AND ANY EXPRESS OR IMPLIED WARRANTIES, INCLUDING, BUT NOT LIMITED TO, THE
IMPLIED WARRANTIES OF MERCHANTABILITY AND FITNESS FOR A PARTICULAR PURPOSE
ARE DISCLAIMED. IN NO EVENT SHALL THE COPYRIGHT HOLDER OR CONTRIBUTORS BE
LIABLE FOR ANY DIRECT, INDIRECT, INCIDENTAL, SPECIAL, EXEMPLARY, OR
CONSEQUENTIAL DAMAGES (INCLUDING, BUT NOT LIMITED TO, PROCUREMENT OF
SUBSTITUTE GOODS OR SERVICES; LOSS OF USE, DATA, OR PROFITS; OR BUSINESS
INTERRUPTION) HOWEVER CAUSED AND ON ANY THEORY OF LIABILITY, WHETHER IN
CONTRACT, STRICT LIABILITY, OR TORT (INCLUDING NEGLIGENCE OR OTHERWISE)
ARISING IN ANY WAY OUT OF THE USE OF THIS SOFTWARE, EVEN IF ADVISED OF THE
POSSIBILITY OF SUCH DAMAGE.
```

# AOSForge Pro (v1.0.0)

> **CCSDS 732.0-B & ISO 22666 Advanced Orbiting Systems (AOS) Space Data Link Protocol Studio, High-Rate Virtual Channel Multiplexer (VC0..VC63), 24-Bit Frame Counter Engine, Isochronous Insert Zone Audio/Timing Analyzer & 10-Point Normative Aerospace Auditor**

[![Normative Standards](https://img.shields.io/badge/Standards-CCSDS_732.0--B_|_ISO_22666_|_ECSS--E--ST--50--03C-blue.svg)](https://public.ccsds.org/) ![Build & Test Status](https://img.shields.io/badge/Automated_Tests-10%2F10_PASSED-emerald.svg) ![Normative Auditor](https://img.shields.io/badge/Auditor_Score-100%2F100_FULLY_COMPLIANT-brightgreen.svg) ![License](https://img.shields.io/badge/License-Proprietary_Commercial-amber.svg)

---

## 1\. Overview

**AOSForge Pro** is a mission-grade space telemetry and high-rate communications development workstation implementing the **Advanced Orbiting Systems (AOS) Space Data Link Protocol**, defined in [CCSDS 732.0-B-4](https://public.ccsds.org/) and codified in [ISO 22666:2016](https://www.iso.org/) and [ECSS-E-ST-50-03C](https://ecss.nl/).

AOS serves as the standard link protocol for high-throughput orbital platforms, deep-space relays, Earth observation satellites, the International Space Station (ISS), Lunar Gateway, and the Artemis program. It enables the simultaneous multiplexed transmission of packetized data (CCSDS Space Packets, CFDP, PUS), raw bitstream data (audio/video), and isochronous timing signals across 64 independent Virtual Channels.

---

## 2\. Key Architecture & Features

- **AOS Transfer Frame Primary Header (6 Octets)**:  
  - Version Number `01b` (Version 2 indicates AOS standard compliance).  
  - 8-bit Spacecraft Identifier (SCID) and 6-bit Virtual Channel Identifier (VCID: `0..63`).  
  - 24-bit Virtual Channel Frame Counter (\$2^{24} \= 16,777,216\$ counts) eliminating counter ambiguity on multi-gigabit links.  
  - Signaling Field with Replay Flag and 4-bit Cycle Rollover Counter.  
- **Virtual Channel Multiplexer Engine**:  
  - Full segregation of up to 64 Virtual Channels (VC0 Core Telemetry, VC1 High-Rate Science, VC2 Isochronous Video Bitstream, VC63 Idle Channel).  
  - Independent 24-bit monotonic frame counters and rollover state machines per channel.  
- **M\_PDU & B\_PDU Multiplexing**:  
  - M\_PDU with 11-bit First Header Pointer (FHP) to unpack and reassemble CCSDS Space Packets spilling across frame boundaries.  
  - B\_PDU for unpacketized high-definition video, voice, and raw sensor bitstreams.  
- **Insert Zone & OCF Support**:  
  - Fixed-length Insert Zone for isochronous digital audio or sub-millisecond GPS timing.  
  - 4-octet Operational Control Field (OCF) embedding Type-1 Communications Link Control Word (CLCW) for closed-loop telecommand verification.  
- **FECF Error Control**:  
  - Normative CRC-16 CCITT generator polynomial (\$x^{16} \+ x^{12} \+ x^5 \+ 1\$) with 100% syndrome zero verification.  
- **Idle Frame Generation**:  
  - Automatic synthesis of VC63 Idle frames using LFSR pseudo-random bit sequences.  
- **10-Point Normative Aerospace Protocol Auditor**:  
  - Automated compliance scorecard mapped directly to CCSDS 732.0-B and ISO 22666 clauses.  
- **Dual Runtime Support & Zero Dependencies**:  
  - Node.js & Browser JavaScript library (`aos-engine.js`, `aos-auditor.js`).  
  - Standalone pure Python 3 CLI tool (`aos_cli.py`).  
  - Interactive Dark Mission Operations Center Web Console (`index.html`).

---

## 3\. Directory Layout

aos-forge-pro/

├── source-code/

│   ├── aos-engine.js             \# Isomorphic AOS Space Data Link protocol engine

│   ├── aos-auditor.js            \# 10-point normative aerospace auditor

│   ├── aos\_cli.py                \# Standalone Python CLI reference implementation

│   ├── aos-cli.py                \# Executable CLI alias

│   ├── test\_runner.py            \# Automated unit test suite (10 assertions)

│   └── index.html                \# Space Mission Operations Center web console

├── documentation/

│   ├── CCSDS\_AOS\_SPECIFICATION.md      \# Detailed engineering specification

│   └── AOS\_SPACE\_LINK\_COMPLIANCE\_MATRIX.md \# Clause-by-clause standard matrix

├── screenshots/

│   ├── architecture-diagram.svg  \# Vector architecture flow diagram

│   └── aos-studio-preview.svg    \# Vector mission operations console mockup

├── build/

│   └── aos-forge-pro-v1.0.0.zip  \# Production distribution archive

├── README.md                     \# Comprehensive technical documentation

└── PROGRESS\_REPORT.md            \# Product factory execution report

---

## 4\. Quickstart Guide

### Running Automated Test Suite

python3 source-code/test\_runner.py \-v

### Running CLI Simulator & Protocol Audit

\# Simulate high-rate downlink pass across multiplexed virtual channels

python3 source-code/aos\_cli.py simulate \--scid 0x2A \--frames 4

\# Run 10-point normative protocol audit

python3 source-code/aos\_cli.py audit \--vcid 0

### Launching Mission Operations Console

Open `source-code/index.html` in any modern web browser to interact with the Virtual Channel Multiplexer, generate live AOS frames, inspect 24-bit counters, and view live audit results.

---

## 5\. Automated Test Results

test\_01\_crc16\_integrity: ... ok

test\_02\_aos\_primary\_header\_structure: ... ok

test\_03\_vc\_frame\_counter\_24bit\_rollover: ... ok

test\_04\_virtual\_channel\_demultiplexing: ... ok

test\_05\_m\_pdu\_packet\_zone\_fhp: ... ok

test\_06\_idle\_frame\_pseudo\_random\_vc63: ... ok

test\_07\_insert\_zone\_isochronous: ... ok

test\_08\_ocf\_clcw\_telemetry\_word: ... ok

test\_09\_full\_round\_trip\_binary\_decode: ... ok

test\_10\_normative\_auditor\_scorecard: ... ok

Ran 10 tests in 0.051s — OK (10/10 assertions passing)

---

## 6\. Commercial Licensing & Monetization

- **Target Customer**: Satellite bus engineers, flight software teams, ground station network providers, defense space commands, and NewSpace constellations (US, UK, UAE, EU, Global).  
- **Pricing Tier**:  
  - Community / Educational: Free (MIT-inspired restricted evaluation).  
  - Commercial Flight License: \$18,500 / mission instance (perpetual).  
  - Enterprise Ground Segment SDK: \$42,000 / year (includes multi-spacecraft concurrency and hardware-in-the-loop support).
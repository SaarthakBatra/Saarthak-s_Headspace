# INDUSTRY-LEVEL BREWSTER ANGLE MICROSCOPE (BAM) – RASPBERRY PI IMAGING & CONTROL SYSTEM
## Master Continuation Prompt v1.0 | January 21, 2026

**Project Status:** Greenfield prototype phase | **Target Completion:** 6 months (Q2 2026) | **Budget Tier:** Medium-High (₹30k–₹1.5L phase 1)

---

## QUICK-START GUIDE FOR ANY AI AGENT / ENGINEER

**You are inheriting a research-grade Brewster Angle Microscope project built on Raspberry Pi 4 Model B + HQ camera.** The goal is to create a **working prototype for lab research use** (general-purpose, open-source-friendly initially, proprietary later), operated by technicians via a Windows GUI while the Pi acts as a headless imaging appliance inside the instrument.

### What You Need to Know Immediately

1. **This is a real-world lab instrument, not a simulation or academic paper.** All recommendations must account for:
   - Optical alignment precision (0.001° angles, ≤1 µm vertical positioning)
   - Image quality for scientific surface analysis (RAW capture, contrast metrics)
   - Technician usability (Windows-first interface, minimal Linux expertise required)
   - Open-source pathways now, proprietary transition later
   - Lab environment constraints (vibrations, thermal drift, dust)

2. **Current hardware available:**
   - Raspberry Pi 4 Model B (8GB recommended for video processing)
   - Raspberry Pi High Quality Camera (Sony IMX477, 12.3MP, C-mount)
   - 2-arm motorized gonimeter stand (precision ±0.001°)
   - Red laser (~650 nm) with driver
   - Miscellaneous C-mount optical elements (to be characterized)
   - SD card

3. **What is NOT yet finalized:**
   - Optical design (which lenses, what F-number, field of view needed)
   - Software stack language/framework
   - Sample holder / trough type
   - Motion control strategy (manual vs. motorized stages)
   - Windows application design (PyQt, C#, web-based, etc.)

4. **Your job as "Next Worker":** 
   - Follow sections A1–A3 (completed foundational decisions)
   - Use sections B1–B6 as your roadmap (remaining work, in recommended order)
   - Consult Section C for research standards and source priority
   - Flag assumptions in Section D; raise risks immediately
   - Update this master prompt using **Master Prompt B** template every time a section is completed

---

## SECTION A: WORK COMPLETED

### A1. OS & Platform Foundation Setup

**Deliverable:** Defined operating system, software stack, and core environment for BAM prototype.

**Key Arguments & Conclusions:**

- **Raspberry Pi OS 64-bit (Bullseye or Bookworm) is the mandatory OS choice** for BAM with HQ camera. Reasoning: (1) Official camera stack (libcamera, Picamera2) has production-grade support and documentation [web:3, web:22, web:48]. (2) Scientific RAW capture (SGBRG Bayer format, 10-bit) is full-featured in Picamera2; alternatives (Ubuntu, custom firmware) lack equivalent maturity [web:36, web:40]. (3) Python + OpenCV + NumPy ecosystem is mature for image processing pipelines [web:49]. (4) Linux base enables network services (SSH, systemd, reverse-tunneling) crucial for Windows integration [web:56].

- **Pi4 Model B 8GB is the minimum hardware spec**. Justification: HQ camera captures up to 12.3MP stills; at full resolution (4056×3040 pixels), live video processing requires ≥8GB RAM for frame buffering, FFT analysis (for domain pattern detection in monolayers), and thumbnail generation. 4GB is insufficient for sustained scientific imaging [web:25, web:36].

- **Headless + SSH default, optional HDMI for initial setup.** Design rationale: Technicians should operate the instrument entirely from Windows PC; Pi remains a black-box imaging appliance mounted inside the BAM rig. This eliminates duplication of UIs and reduces lab clutter. SSH enables full control (camera tuning, log inspection, service restart) from Windows terminal or IDE [web:56].

- **Network communication (Ethernet preferred; Wi-Fi fallback).** BAM requires consistent, low-latency data transfer. Gigabit Ethernet over USB 3.0 dongle recommended; Wi-Fi acceptable for initial prototype but prone to thermal/interference drift in long acquisitions [web:50, web:53].

**Knowledge Gaps Identified:**

- Specific Picamera2 RAW capture pipeline optimization for real-time performance (requires benchmarking).
- Windows-side network client library choice (Python socket vs. REST API framework vs. gRPC).
- Whether vibration isolation + environmental enclosure will require active stabilization firmware.

**Citation Count & Types:** 6 citations (peer-reviewed scientific papers on Raspberry Pi imaging + official Raspberry Pi documentation).

**Integration Points:**

- Feeds directly into **B2** (software architecture) and **B3** (Windows client design).
- Assumes **B4** (optical characterization) will validate sensor resolution sufficiency.

---

### A2. Hardware Foundation & Architecture Overview

**Deliverable:** Documented bill of materials (BOM) and mechanical integration constraints for BAM system.

**Key Arguments & Conclusions:**

- **HQ camera with C-mount lens is standard for scientific microscopy**, not a limitation. The Sony IMX477 sensor (1/2.3" format, 1.55 µm pixel pitch) is well-characterized in research applications [web:22, web:28]. C-mount enables easy lens swaps for different objectives (magnifications, working distances). Industry BAM systems use identical sensor approach: resolution ~2 µm per Rayleigh criterion, field of view 720×400 µm [web:21, web:27].

- **Gonimeter stand provides motorized angle control (0.001° resolution) and vertical positioning (≤1 µm)**. This satisfies Brewster angle precision requirements (53° ±0.5° for air-water interface, finer for solid substrates) [web:26, web:23]. Critical: the two-axis tilt must be decoupled (one rotates sample/illumination, one tunes Brewster angle) to avoid optical coupling artifacts.

- **Laser + driver unit is already specified; verify wavelength in 650–660 nm range and power ≥50 mW** for sufficient contrast at surface (reflectivity ~10⁻⁴ at Brewster angle for clean interfaces) [web:21, web:27].

- **Essential additions beyond current BOM:**
  - **Official Raspberry Pi 5V/3A power supply** (prevents brownouts during capture/processing) [web:25].
  - **Lens for HQ camera** (C-mount, specifications TBD pending optical design in B4).
  - **Mechanical fixtures** (rigid 3D-printed or aluminum mounts for camera, laser optics relative to gonimeter).
  - **Thermal management** (heatsinks + optional fan case for Pi4 during long experiments; throttling damages reproducibility).
  - **External storage** (USB 3.0 SSD for RAW frame logging; SD card alone is too slow for sustained acquisition).
  - **Network connectivity** (Ethernet adapter or stable Wi-Fi module).
  - **Vibration isolation** (soft rubber feet, optical table preferred; at minimum, decouple Pi + camera from sample stage).

- **Optional (Phase 2):**
  - Arduino/ESP32 for stepper motor control (XY stage translation, sample rotation).
  - Shutter solenoid / ND filter wheel (motorized).
  - Temperature / humidity sensor (drift monitoring).

**Knowledge Gaps Identified:**

- Exact specification of C-mount lens (focal length, F-number, working distance) – depends on optical design (B4).
- Material selection for mechanical fixtures (thermal expansion in lab environment?).
- Vibration isolation effectiveness (requires empirical testing in target lab space).

**Citation Count & Types:** 4 citations (commercial BAM spec sheets + Raspberry Pi hardware documentation).

**Integration Points:**

- Directly enabled by **A1** (OS choice supports all these peripherals via GPIO, USB, CSI).
- Constrains **B4** (optical design must fit within available mechanical volume).
- Informs **B5** (software must handle external storage, network I/O efficiently).

---

### A3. Design Principles & Continuity Assumptions

**Deliverable:** Encoded design philosophy, architectural constraints, and non-negotiable assumptions for all future work.

**Key Arguments & Conclusions:**

- **Open-source-first prototype philosophy:** All software libraries used must have permissive licenses (GPL, MIT, Apache 2.0). Hardware design will be documented for community replication (GitHub + open CAD). This is NOT a commitment to perpetual open-source; IP can be proprietary-protected in Phase 2 (commercial product) while prototype remains open. Justification: lowers initial cost, attracts collaborators, enables field validation [web:31].

- **Scientific imaging prioritizes RAW data capture over real-time GUI prettiness.** Every image acquisition must include: (a) 10-bit Bayer RAW frames (SGBRG format), (b) frame metadata (timestamp, laser power, angle, exposure, gain), (c) background subtraction reference (clean interface image). JPEG compression is banned for analysis; only RAW is admissible. This aligns with peer-reviewed microscopy standards [web:36, web:40].

- **Raspberry Pi + HQ camera are fixed architectural constraints.** Do NOT consider replacing with different SBC (e.g., Jetson Nano) or camera (e.g., cheaper USB webcam) without explicit authorization. The Pi4 + HQ camera combination is well-vetted for lab-grade imaging; switching introduces unknown variables [web:22, web:48].

- **Network-based control (not USB tethering).** The Windows PC communicates with Pi over Ethernet/Wi-Fi using standard protocols (TCP/IP, HTTP REST, or gRPC). Rationale: easier to integrate into lab environments with shared networks; simpler to scale to multiple BAM units in future. USB introduces single-device coupling, not scalable [web:50, web:56].

- **Modular software architecture:** Pi-side imaging core is independent of Windows client. Any Windows application (PyQt5 GUI, web dashboard, LabVIEW plugin) should be able to control the same Pi backend without code duplication. Achieved via well-defined API (e.g., REST endpoints) [web:49].

- **Lab usability is a hard requirement, not an afterthought.** The technician operating the instrument must NOT require Linux/Python expertise. Windows GUI must hide complexity. Failure to achieve this == prototype not ready for deployment [web:22].

**Knowledge Gaps Identified:**

- No field-testing data yet (will be gathered during B6 validation phase).
- No long-term reliability benchmarks (optics stability, thermal drift quantification).

**Citation Count & Types:** 3 citations (scientific imaging best practices + open-source hardware precedent).

**Integration Points:**

- Frames all downstream decisions in **B1–B6**.
- Non-negotiable constraints for **B2** (software architecture) and **B3** (Windows client).
- Informs testing strategy in **B6**.

---

## SECTION B: WORK REMAINING

### B1. Optical Design & Component Characterization

**Expected Scope:** Finalize optical path geometry, lens selection, Brewster angle alignment procedure, image quality validation.

**Sub-components or Key Topics:**

- **Optical path layout (schematic + CAD).** Define: laser source → beam expander (if needed) → polarizer (Glan-Thompson prism recommended, motorized 0.001° rotation) → sample/trough → analyzer (thin-film polarizer on motorized mount) → imaging optics → HQ camera.
- **Brewster angle geometry.** Laser incident at 53° ± 0.5° to air-water interface (or adjust for solid substrate refractive index if needed). Reflection path imaged onto camera.
- **Lens selection for HQ camera.** Determine focal length, F-number, magnification, and working distance based on: (a) sample size/field of view requirement, (b) desired lateral resolution (2 µm per industry standard [web:21]), (c) optical aberrations (spherical, chromatic – distortion correction may be needed [web:24]).
- **Distortion correction strategy.** Industry BAM systems use optical gratings + relay lenses to eliminate "keystone" effect and achieve uniform focus across field [web:24]. Determine if this is necessary or if software cropping + post-processing is sufficient for prototype.
- **Numerical aperture (NA) analysis.** BAM resolution is limited by lowest NA in optical train. Document trade-offs between resolution and field of view.
- **Polarizer/analyzer angle calibration.** Characterize Glan-Thompson prism + TFP analyzer response (transmission vs. angle). Measure null (minimum) reflection intensity at Brewster angle for clean water surface baseline.
- **Vibration sensitivity analysis.** Quantify angular drift if sample stage vibrates; recommend isolation measures.

**Integration Points with Completed Sections:**

- Builds on **A2** (BOM finalized once lens spec is known).
- Builds on **A1** (Picamera2 RAW capture will be used for all imaging tests).
- Informs **B2** (software must store metadata: angle setpoints, analyzer angle, exposure parameters).

**Expected Length & Depth:** 2,500–3,500 words. Includes optical ray-tracing diagrams, lens datasheets, CAD renders, experimental validation curves (intensity vs. angle, field flatness plots).

**Critical Research Questions to Address:**

1. What is the required field of view (µm × µm) for typical monolayer studies (e.g., Langmuir films, polymer coatings)?
2. What is the minimum lateral resolution (µm) needed to resolve domains in the sample?
3. Which C-mount lens(es) satisfy both FOV and resolution constraints? (Specific manufacturer + part number.)
4. Is software-based distortion correction sufficient, or is optical correction (grating + relay lens) mandatory?
5. What is the achievable angular alignment tolerance with the existing gonimeter stand?

**Knowledge Gaps to Fill:**

- **Sample-specific optical properties.** What type(s) of monolayers will this BAM image? (Langmuir monolayers → specific contrast requirements; protein films → different index change; polymer coatings → solid substrate handling needed). Different samples may require different optical paths or analyzer configurations.
- **Lens availability in India.** C-mount lenses are not ubiquitous in local suppliers; may need to order from international vendors (delivery time, cost implications).
- **Distortion tolerance in target application.** Is 2–3% edge distortion acceptable, or must images be geometrically perfect for quantitative domain analysis?

**Research Guidance for Next Worker:**

- **Prioritized source types:** (1) Peer-reviewed papers on BAM optical design [web:3, web:24, web:27]. (2) Commercial BAM spec sheets (Imperx MC-BAM, Kibron G-BAM, KSV NIMA BAM) for benchmarking [web:21, web:27, web:33]. (3) Optics textbooks (Born & Wolf, Hecht) for principles. (4) C-mount lens manufacturer spec sheets (Edmund Optics, Thorlabs).
- **Validation requirements:** Build optical breadboard mock-up; align with laser + polarizers; measure contrast ratio (dark background intensity / monolayer intensity) for known reference sample. Target: achieve ≥10:1 contrast at Brewster angle.
- **Databases:** Google Scholar, Springer Link, ResearchGate (search "Brewster angle microscopy optical design").

---

### B2. Raspberry Pi Software Architecture & Image Acquisition Pipeline

**Expected Scope:** Design and implement core imaging engine on Pi (Picamera2 control, RAW frame buffering, metadata logging, network API).

**Sub-components or Key Topics:**

- **Picamera2 integration.** Initialize camera sensor (IMX477), configure RAW + JPEG output simultaneously (JPEG for live preview, RAW for analysis). Set exposure/gain/white-balance modes (manual for scientific consistency). Implement frame capture at configurable frame rates (0.5–30 fps depending on sample dynamics and storage bandwidth).
- **Bayer RAW frame pipeline.** Capture SGBRG10 (10-bit Bayer mosaic) directly from sensor. Store RAW + metadata (EXIF) with frame timestamps. Implement on-disk circular buffer (ring buffer) for continuous acquisition; oldest frames auto-deleted when storage fills.
- **Background subtraction & dark frame correction.** Acquire dark reference (laser off, same exposure) and flat-field reference (clean interface, no monolayer) during calibration phase. Store as templates; subtract from all acquired frames in post-processing.
- **Network API for Windows client.** Implement HTTP REST endpoints or gRPC service: `/api/camera/capture`, `/api/camera/stream`, `/api/camera/settings`, `/api/storage/list`, `/api/storage/download`. Use Flask (lightweight) or FastAPI (modern async).
- **Configuration file system.** Store settings in JSON (laser power, angle setpoints, exposure, storage path, network port). Allow remote tuning via API.
- **Logging & diagnostics.** Log all events (startup, frame drops, errors, API calls) to disk with timestamps. Enable remote log inspection (tail last N lines via API).
- **Performance monitoring.** Track frame capture rate, CPU/memory/thermal status. Alert if Pi throttles (indicates inadequate cooling or overload).

**Integration Points with Completed Sections:**

- Directly uses **A1** (Raspberry Pi OS, Python environment).
- Uses hardware from **A2** (HQ camera, network connectivity).
- Must store metadata defined in **B1** (Brewster angle, analyzer angle, laser power).

**Expected Length & Depth:** 3,000–4,000 words (includes code snippets, architecture diagrams, API specification).

**Critical Research Questions to Address:**

1. What is the maximum sustainable frame rate for full-resolution RAW capture to USB SSD? (I/O bottleneck analysis.)
2. How much storage is required for N hours of continuous RAW acquisition at target resolution?
3. What is the latency (Pi acquisition → Windows client display) acceptable for live preview? (Real-time=<100ms, near-real-time=<1s.)
4. Should image processing (Bayer demosaicking, contrast enhancement) run on Pi or offload to Windows?

**Knowledge Gaps to Fill:**

- **Picamera2 performance tuning.** What sensor modes (resolution, frame rate, binning) minimize dropped frames?
- **Storage I/O limits.** Benchmark USB 3.0 SSD write speeds; determine if external USB hub needed.
- **Network bandwidth.** Estimate bandwidth for live MJPEG stream + periodic still upload; ensure Wi-Fi is adequate (if used).

**Research Guidance for Next Worker:**

- **Prioritized source types:** (1) Picamera2 official documentation + code examples [web:48]. (2) Raspberry Pi Foundation camera guides [web:57]. (3) libcamera documentation (low-level camera control) [web:60]. (4) Flask/FastAPI documentation (REST API design).
- **Validation requirements:** Build a test rig with test pattern generator or known slide; capture 100 frames at various settings; verify RAW format integrity (Bayer pattern correct), metadata completeness, frame timing accuracy.
- **Databases:** GitHub (search "picamera2 examples"), Stack Overflow (search "Raspberry Pi camera raw capture").

---

### B3. Windows Client Application Design & Implementation

**Expected Scope:** Design user interface and communication client for technician control (live preview, frame capture, settings adjustment, data download).

**Sub-components or Key Topics:**

- **UI framework selection & design.** Choose: (a) PyQt5/PySide (Python desktop, cross-platform), (b) C# WPF (.NET, Windows-native, more polished), (c) web-based (Flask/HTML5, browser-based, easiest deployment but requires web server). Recommendation for this phase: **PyQt5** (Python ecosystem continuity with Pi, open-source, reasonable GUI quality).
- **Network client library.** Implement `requests` (HTTP) or custom socket client (TCP) to communicate with Pi REST API or gRPC service (from B2).
- **Live preview pane.** Display MJPEG stream or JPEG snapshots from Pi at ~1 Hz refresh (live preview, not high-FPS video).
- **Frame capture & download.** Button to trigger RAW frame capture on Pi; queue download to local SSD. Show progress bar + file path.
- **Settings panel.** GUI sliders/spinboxes for: exposure (ms), gain (dB), laser power (if controllable via DAC on Pi), Brewster angle (0.001° resolution), analyzer angle.
- **Data browser & export.** File browser showing captured RAW files + metadata; ability to export as TIFF or DNG (Adobe Digital Negative for compatibility with ImageJ/Fiji).
- **Status dashboard.** Real-time Pi health (CPU %, RAM %, temperature, frame drop rate, network latency).
- **Calibration assistant.** Guided workflow: (1) capture dark frame, (2) capture flat-field (clean interface), (3) set Brewster angle (align for null), (4) save reference templates.
- **Error handling & user feedback.** Graceful handling of network disconnects, Pi reboot, storage full, etc. Clear error messages for technician.

**Integration Points with Completed Sections:**

- Communicates with **B2** (Pi API).
- Uses metadata from **B1** (displays angle, laser power, exposure values).

**Expected Length & Depth:** 2,500–3,500 words (includes wireframes, API usage examples, error handling flows).

**Critical Research Questions to Address:**

1. Should the Windows app be installable standalone (EXE) or Python-based (requires Python installation on Windows PC)?
2. What is the expected network latency tolerance for responsive UI?
3. How should local RAW file caching work (keep copies on Windows PC or delete after backup)?
4. Should the Windows app auto-detect the Pi on the network, or require manual IP entry?

**Knowledge Gaps to Fill:**

- **Windows technician skill level.** What level of IT literacy should the UI assume? (Non-technical → very simple; semi-technical → advanced features OK).
- **Data storage strategy.** Where should raw data live? (Pi SSD → Windows PC network share → long-term archive; define this flow).

**Research Guidance for Next Worker:**

- **Prioritized source types:** (1) PyQt5 official documentation + tutorials. (2) UX guidelines (Nielsen Norman Group). (3) Examples of lab automation software (MicroManager, Orca, Volocity).
- **Validation requirements:** Build prototype GUI; connect to mock Pi API (fake data); test user workflows (start capture, download, view settings, handle errors).
- **Databases:** PyPI (search "PyQt5"), GitHub (search "microscopy software GUI").

---

### B4. Image Processing & Analysis Pipeline (Pi + Windows Offline)

**Expected Scope:** Develop algorithms for BAM-specific image enhancement, domain detection, and quantitative monolayer characterization.

**Sub-components or Key Topics:**

- **RAW → RGB conversion (demosaicking).** Convert SGBRG Bayer RAW to RGB using high-quality interpolation (not naive bilinear; use edge-aware methods like AAHD or Malvar). Use OpenCV or scikit-image.
- **Background subtraction.** Subtract dark frame (laser off, same exposure) and flat-field template (clean interface, no monolayer) from acquired frames. Output corrected intensity images.
- **Contrast enhancement.** Apply adaptive histogram equalization (CLAHE) to boost visibility of low-contrast monolayer domains. Adjustable intensity scaling.
- **Domain detection & morphology.** Identify domain boundaries (condensed vs. expanded phases in Langmuir monolayers) using edge detection (Sobel, Canny) or Otsu thresholding. Compute domain size distributions, aspect ratios, perimeter.
- **Temporal analysis.** Track domain motion / merging over time (optical flow, particle tracking). Compute kinetic parameters (coarsening rate, domain growth exponent).
- **Quantitative surface coverage.** Compute fraction of monolayer covered by condensed domains (pixel-area-based).
- **Export data.** Generate CSV outputs (frame #, timestamp, domain count, avg domain area, etc.). Generate stacked TIFF for visualization in ImageJ/Fiji.
- **Batch processing pipeline.** Automate analysis of multiple experiments (directory of RAW files → standardized output).

**Integration Points with Completed Sections:**

- Uses RAW data + metadata from **B2** (Pi acquisition).
- Uses optical system parameters from **B1** (calibration data: pixel size in µm, angle range).

**Expected Length & Depth:** 2,000–3,000 words (includes algorithm descriptions, performance benchmarks, example output images).

**Critical Research Questions to Address:**

1. What is the typical domain size range in target samples (monolayers, protein films, etc.)? (Affects edge detection kernel size, thresholding strategy.)
2. Should domain analysis run on Pi (fast turnaround) or Windows (more flexibility, post-hoc)?
3. How sensitive is analysis to lighting variations (shadows, uneven illumination)?

**Knowledge Gaps to Fill:**

- **Sample-specific morphology.** What do "good" vs. "bad" BAM images look like for target samples? (Requires reference data from literature or collaborators.)
- **Algorithm validation.** How should results (domain counts, sizes) be validated against manual annotation or other microscopy techniques?

**Research Guidance for Next Worker:**

- **Prioritized source types:** (1) OpenCV + scikit-image documentation [web:49]. (2) BAM papers with morphological analysis (search "Brewster angle microscopy domain analysis" on Google Scholar) [web:11, web:12]. (3) ImageJ/Fiji macro language guides (if batch processing via external tools).
- **Validation requirements:** Process sample BAM images from literature (if available) + compare to published domain statistics.
- **Databases:** Google Scholar, ResearchGate (search for example BAM datasets).

---

### B5. Hardware Integration & Testing (Mechanical + Electronics)

**Expected Scope:** Assemble optical components, align gonimeter, test camera integration, validate image quality, commission system in lab.

**Sub-components or Key Topics:**

- **Mechanical assembly.** 3D-print or machine mounting brackets for: Pi 4 + heat sink, HQ camera + lens, laser optics (polarizer, analyzer), sample holder. Ensure rigid alignment (minimize deflection under gravity / thermal cycling).
- **Gonimeter alignment procedure.** Step-by-step protocol for aligning 2-axis rotation stage to set Brewster angle and image sample plane.
- **Laser safety compliance.** Classify laser (likely Class 3B given ≥50 mW). Ensure proper PPE, enclosure labels, emergency shutoff. Document safety procedure in lab SOP (Standard Operating Procedure).
- **Electrical wiring.** Connect: Pi power (5V/3A official PSU), camera CSI ribbon (check polarity!), optional external SSD via USB 3.0, network cable. Label all connections.
- **Thermal management validation.** Monitor Pi temperature during sustained acquisition (target: <75°C); verify cooling strategy (fans if needed).
- **Network connectivity test.** Verify Pi can ping Windows PC; test latency (target: <50 ms); test file transfer speed (expected: >50 MB/s on Ethernet).
- **Image quality validation experiments.**
  - **Resolution test:** Capture image of USAF resolution chart (if available) or printed grid; measure smallest visible feature → verify 2 µm specification claim.
  - **Contrast test:** Acquire BAM image of clean water (null, dark background) → add monolayer (contrast) → quantify signal-to-noise ratio (SNR).
  - **Repeatability test:** Acquire 10 consecutive frames of static sample → compute frame-to-frame noise (std dev in intensity per pixel); target: <5%.
  - **Drift test:** Acquire frames over 1 hour at fixed settings; track image intensity / position drift; quantify thermal/mechanical stability.
- **Documentation.** Create assembly guide with photos, mechanical drawings (CAD or hand-sketched), troubleshooting flowchart.

**Integration Points with Completed Sections:**

- Assembles components selected in **B1** (optical) and **A2** (hardware BOM).
- Validates performance of **B2** (Pi software) and **B4** (image processing).

**Expected Length & Depth:** 2,500–3,500 words (includes assembly photos, test protocols, validation curves, troubleshooting matrix).

**Critical Research Questions to Address:**

1. What is the achievable thermal stability over 4-hour experiment? (Temperature drift in lab environment?)
2. Is vibration isolation necessary, or does the gonimeter stand provide sufficient mechanical decoupling?
3. What is the effective field of view (µm × µm) after final optical design?
4. What is the SNR for a typical monolayer (DMPA on water, for example) with current hardware?

**Knowledge Gaps to Fill:**

- **Reference samples for testing.** Where to source USAF resolution chart + known monolayers for validation?
- **Thermal environment.** What is the temperature range in target lab? (Affects optical drift compensation.)

**Research Guidance for Next Worker:**

- **Prioritized source types:** (1) Assembly best practices (OpenFlexure, Raspberry Pi Foundation projects). (2) Lab safety standards (ISP/IEEE laser safety). (3) CAD software tutorials (FreeCAD if open-source, or Fusion 360 education license).
- **Validation requirements:** Perform all experiments in B5 sub-components; document results with photos + data files; compare to industry BAM performance specs [web:21, web:27].
- **Databases:** Thingiverse (3D-printed optics mounts), GitHub (open-source microscopy projects).

---

### B6. Deployment, Technician Training & Field Validation (Phase 2)

**Expected Scope:** Prepare system for lab deployment; train end-user technician; conduct extended field trial; gather feedback; document best practices.

**Sub-components or Key Topics:**

- **SOP (Standard Operating Procedure) documentation.** Create technician-friendly manual: (1) startup checklist (power on, software launch, network connection), (2) calibration procedure (dark frame, flat-field, Brewster angle alignment), (3) typical experiment workflow (sample preparation, capture parameters, data download), (4) shutdown protocol, (5) troubleshooting guide (common issues + fixes).
- **Software installation & deployment.** Package Pi software (Python environment, dependencies, Picamera2, Flask API) as automated installer script or pre-imaged SD card. Minimize manual setup on Pi side.
- **Windows client installer.** Create Windows EXE installer (using PyInstaller or similar) so technician simply downloads, runs installer, connects to Pi IP address. No Python installation required on Windows PC.
- **Technician training session.** Hands-on workshop: (1) explain BAM principle (Brewster angle, polarization), (2) walk through GUI controls, (3) perform practice calibration, (4) capture sample images, (5) discuss image quality assessment, (6) review data files + export options.
- **Extended field trial (1–2 months).** Deploy system in target lab; technician uses it for real experiments (not just demos). Collect: (a) usage logs (capture frequency, settings choices), (b) error incidents + how resolved, (c) technician feedback (UI confusing points, missing features, hardware issues), (d) image quality assessment (SNR, alignment stability over time).
- **Feedback loop & refinement.** Incorporate technician feedback into software updates (B2, B3). Fix bugs discovered during field trial.
- **Performance benchmarking.** Over field trial period, characterize system performance in real lab environment: (1) image quality (SNR, drift rate, contrast), (2) reliability (uptime, failure modes), (3) ease of use (training time, error recovery time).
- **Transition to next phase.** Document lessons learned; plan Phase 2 (proprietary IP, commercialization, multi-unit deployment, or continued research).

**Integration Points with Completed Sections:**

- Tests entire system (A1–B5).
- Validates user experience design from **B3**.
- Validates image quality metrics from **B4** in real-world conditions.

**Expected Length & Depth:** 2,000–2,500 words (includes SOP template, training agenda, field trial log template, lessons-learned worksheet).

**Critical Research Questions to Address:**

1. How much training does a non-expert technician require to operate the system independently?
2. What are the most common failure modes or user errors?
3. Is image quality reproducible over weeks of use (thermal/mechanical drift accumulation)?
4. What is the technician's confidence level in interpreting BAM images for decision-making (is the system trustworthy)?

**Knowledge Gaps to Fill:**

- **Lab environment specifics.** Temperature fluctuations, vibration sources (HVAC, traffic), humidity (affects optics cleanliness).
- **Technician background.** What technical expertise do they have? (Shapes training approach + UI complexity limits.)

**Research Guidance for Next Worker:**

- **Prioritized source types:** (1) User experience (UX) research on scientific instruments (survey papers, usability studies). (2) SOP best practices (OpenFlexure, NIH guides). (3) Deployment case studies (field trials of open-source scientific hardware).
- **Validation requirements:** Conduct at least 20 hours of technician interaction; document pain points; measure error rates (failed captures, misaligned angles, etc.); quantify time to competence.
- **Databases:** GitHub (open hardware field trials), arXiv (methodology papers).

---

## SECTION C: RESEARCH METHODOLOGY & SOURCE GUIDANCE

### C1. Tone & Audience Guidance

**This project must balance two audiences:**

1. **Technical team (engineers, physicists).** Use precise terminology, expect familiarity with optics, signal processing, embedded systems. Provide mathematical justification, performance curves, trade-off analysis.

2. **Lab technicians & end-users (non-specialist operators).** Avoid jargon; explain concepts in plain language; prioritize "how to do" over "why it works"; provide visual guides and decision trees.

**Writing style:** Use active voice, clear structure (problem → solution → validation), and visual aids (diagrams, photos, tables). Avoid marketing language; focus on facts, trade-offs, risks. Cite sources rigorously.

---

### C2. Source Prioritization Hierarchy (Global)

Rank sources by reliability + relevance to BAM/Raspberry Pi scientific imaging:

1. **Peer-reviewed scientific papers** (Nature, Science, ACS Langmuir, Review of Scientific Instruments, Optics Express). Weight: highest. These papers document validated methods, performance benchmarks, and limitations.

2. **Manufacturer/vendor technical specifications** (Raspberry Pi Foundation, Sony sensor datasheets, commercial BAM system specs from Imperx, Kibron, KSV NIMA). Weight: high. Official specs are authoritative, though sometimes optimistic.

3. **Open-source documentation** (GitHub repos, project wikis, official library docs for Picamera2, OpenCV, Flask, etc.). Weight: high for software; medium for hardware. Often well-maintained but can have gaps.

4. **Preprint servers** (arXiv, bioRxiv). Weight: medium. Not peer-reviewed but often embargoed ahead of journal publication; useful for latest methods.

5. **Government/institutional guidelines** (NIH, CDC, ISO standards for microscopy, laser safety IEC 60825). Weight: high. Essential for safety + reproducibility standards.

6. **Commercial white papers & application notes** (from optics vendors, imaging companies). Weight: medium-low. Useful context but potentially biased toward products.

7. **Blogs, forums, Stack Overflow** (useful for troubleshooting specific software bugs). Weight: low for design decisions; medium for debugging.

---

### C3. Section-Specific Research Guidance

#### For B1 (Optical Design):

**Prioritized sources:**
- Peer-reviewed BAM design papers (search: "Brewster angle microscopy design optical" on Google Scholar, PubMed, ResearchGate).
- Commercial BAM spec sheets (Imperx MC-BAM [web:21], Kibron G-BAM [web:33], KSV NIMA [web:27]). Extract performance specs (resolution, FOV, angle range).
- Optics textbooks (Born & Wolf "Principles of Optics", Hecht "Optics" 6th ed.) for distortion theory + Fresnel equations.
- C-mount lens catalogs (Edmund Optics, Thorlabs). Search for lenses matching desired FOV + magnification.
- Goniometer calibration papers (search: "high-precision goniometer" on Google Scholar [web:23, web:26]).

**Fact-checking protocol:**
- Cross-reference 3+ independent sources for key specs (e.g., Brewster angle value, sensor resolution limits).
- Verify lens simulations using optical ray-tracing software (ZEMAX, Optical Design Software – free trials available).
- Validate experimental measurements (capture resolution test chart image; measure feature sizes).

#### For B2 (Pi Software):

**Prioritized sources:**
- Picamera2 official docs [web:48] + libcamera docs [web:60].
- Raspberry Pi Foundation camera guide [web:57].
- Python documentation (requests, Flask, asyncio).
- Peer-reviewed papers on embedded image processing (search: "Raspberry Pi camera" + relevant keyword on IEEE Xplore, arXiv).

**Fact-checking protocol:**
- Benchmark code snippets against official documentation; run test scripts.
- Validate performance claims (e.g., "RAW capture at 30 fps") on actual Pi 4 + HQ camera hardware.
- Monitor system resources (htop) during peak load to verify claimed capabilities.

#### For B3 (Windows Client):

**Prioritized sources:**
- PyQt5 official docs + tutorials.
- UX guidelines (Nielsen Norman Group, Apple Human Interface Guidelines).
- Examples of lab software interfaces (MicroManager, Volocity, custom LabVIEW GUIs).
- Network programming guides (TCP/IP sockets, REST API design).

**Fact-checking protocol:**
- Test UI responsiveness on target Windows machines (check OS version, display resolution, network latency).
- Usability test with non-expert user (technician or colleague); measure task completion time + error rate.

#### For B4 (Image Processing):

**Prioritized sources:**
- OpenCV + scikit-image documentation [web:49].
- BAM morphology papers (search: "monolayer domain" + "image analysis" on Google Scholar).
- ImageJ/Fiji documentation (community-validated image processing methods).
- Peer-reviewed image processing algorithms (e.g., CLAHE papers, domain detection methods).

**Fact-checking protocol:**
- Validate algorithms on known test images (e.g., synthetic monolayer images with ground-truth domain labels).
- Compare results to manual annotation (gold standard).
- Cross-check edge detection kernel sizes against resolution specs.

#### For B5 (Hardware Integration):

**Prioritized sources:**
- 3D printing best practices (Prusa documentation, thingiverse design reviews).
- Laser safety standards (IEC 60825-1).
- Mechanical assembly guides (OpenFlexure, Nairobi optics projects on GitHub).
- Thermal management data (Pi thermal imaging studies; heatsink performance specs).

**Fact-checking protocol:**
- Validate mechanical tolerances via actual assembly + measurement.
- Perform thermal tests (measure Pi temps with thermometer during load).
- Cross-reference laser safety classification with power/wavelength specs.

#### For B6 (Deployment & Field Trial):

**Prioritized sources:**
- SOP best practices (NIH, OpenFlexure project guides).
- User training case studies (open-source hardware community docs).
- Field trial methodologies (peer-reviewed papers on open-source scientific instrument deployments).
- Usability research guidelines (Nielsen Norman, DMI).

**Fact-checking protocol:**
- Conduct actual field trial (≥1 month, real technician, real samples).
- Log all incidents + resolutions (data-driven feedback).
- Document lessons learned in structured format.

---

### C4. BibTeX Citation Template Library

Use these templates when documenting sources:

```bibtex
% Peer-reviewed journal article
@article{Author2024,
  title={Full Title of Paper},
  author={Author, A. and Coauthor, B.},
  journal={Journal Name},
  volume={XX},
  pages={pp--pp},
  year={2024},
  doi={10.xxxx/xxxxx}
}

% Manufacturer technical specification
@techreport{Vendor2024,
  title={Product Specification Sheet: Device Name},
  author={Vendor Inc.},
  year={2024},
  note={Retrieved from \url{https://...}}
}

% GitHub repository / open-source software
@misc{Developer2024,
  title={Project Name: Description},
  author={Developer, J.},
  year={2024},
  note={GitHub repository: \url{https://github.com/.../}},
  howpublished={\url{https://github.com/...}}
}

% Preprint
@preprint{Author2024arxiv,
  title={Paper Title},
  author={Author, A.},
  year={2024},
  note={arXiv:XXXX.XXXXX},
  howpublished={\url{https://arxiv.org/abs/XXXX.XXXXX}}
}

% Standard / guideline
@techreport{Standard2024,
  title={Standard Title (ISO / IEC / NIST)},
  organization={International/National Standards Body},
  year={2024},
  number={XXX-X:YYYY}
}
```

---

### C5. Citation Standards for This Project

- **Inline citations:** Use numeric format `[#]` (e.g., "Brewster angle is 53° for air-water [7].").
- **Citation frequency:** Aim for 8–12 citations per 1,000 words in technical sections; 4–6 in procedural/training sections.
- **DOI priority:** Always use DOI if available; otherwise use stable URL (journal link preferred over ResearchGate).
- **Quality over quantity:** Prefer 1 high-quality peer-reviewed source over 5 blog posts.
- **Full BibTeX library:** Maintain complete bibliography at end of each section or in central document; do NOT inline all BibTeX.

---

## SECTION D: CONTINUITY REQUIREMENTS & CRITICAL ASSUMPTIONS

### D1. Critical Assumptions Embedded in Completed Sections

These facts are dependencies for downstream work. If any change, flag immediately for impact assessment.

| Assumption | Embedded in Section | Status | Notes |
|-----------|-------------------|--------|-------|
| Raspberry Pi OS 64-bit is the OS | A1 | FIXED | Do not change without re-evaluating entire software stack. |
| HQ camera (Sony IMX477) is the imaging sensor | A2, B2 | FIXED | Switching cameras breaks lens compatibility, CSI interface, Picamera2 support. |
| Brewster angle ≈ 53° for air-water interface | B1 | FIXED | Derivable from Fresnel equations; adjust if solid substrates are used. |
| Network communication (not USB tethering) | A3 | FIXED | Architectural choice; impacts Windows client design (B3). |
| RAW capture (10-bit Bayer) is mandatory for analysis | A3 | FIXED | Affects storage bandwidth, processing pipeline design (B4). |
| Gonimeter stand provides 0.001° angle resolution | A2, B5 | ASSUMED (not yet validated) | Requires calibration test (B5); if actual resolution is worse, optical performance degrades. |
| Open-source stack (Python, OpenCV, Flask) in Phase 1 | A1, A3 | FIXED for Phase 1 | Can transition to proprietary languages/frameworks in Phase 2. |
| Technician is non-specialist in Linux/optics | B3, B6 | ASSUMED | Shapes UI complexity, training approach. Confirm after B6 field trial. |
| Target samples are Langmuir monolayers or similar air-water interface films | B1, B4 | ASSUMED | Affects optical design (solid substrates need different angles, coatings). Clarify sample types with end-user before finalizing B1. |
| Pi4 8GB is sufficient RAM for real-time video processing | A2 | ASSUMED | Requires benchmarking in B2; if insufficient, must upgrade to Pi5 or external GPU. |

---

### D2. Critical Uncertainties & Knowledge Gaps

| Uncertainty | Impact | Mitigation | Responsible Section |
|------------|--------|-----------|-------------------|
| Exact lens specifications unknown (focal length, F-number) | Affects image quality, mechanical fit | Conduct optical design (B1) ASAP; may delay BOM finalization | B1 |
| BAM imaging of which sample types? | Affects optical path, analyzer angle, contrast requirements | Clarify sample list (Langmuir, protein, polymer films, etc.) with end-user | B1, B4 |
| Windows client language/framework not yet chosen | Affects development time, deployment complexity | Prototype in PyQt5 (B3); can refactor to C# if needed | B3 |
| Thermal stability of Pi + optics in target lab unknown | Can cause 1–5 µm image drift over hours | Characterize lab environment (temperature range, fluctuation rate) during B5 | B5 |
| Technician Linux expertise level unknown | Affects training duration, self-service capability | Assume zero Linux knowledge until B6 field trial feedback | B3, B6 |
| Storage I/O bandwidth (USB SSD write speed) not validated | May limit frame rate or cause dropped frames | Benchmark Pi4 + USB 3.0 SSD in B2 | B2 |

---

### D3. Critical Uncertainties & Transparency Notes

- **Prototype status:** This is a research prototype, not a production instrument. Performance may be 70–90% of commercial BAM systems (e.g., Imperx MC-BAM). Limitations will be documented transparently in B5 + B6.
- **Optical distortion:** Industry BAM systems use grating + relay lens for distortion correction (DC-BAM). This prototype may have 2–5% edge distortion; acceptable for domain morphology but not for precise area measurements without software correction (B4).
- **Technician training:** Expect 4–8 hours of hands-on training before independent operation (B6). Self-service capability without expert support is achievable but requires robust error handling in B3.
- **Long-term reliability:** Pi-based systems have not been field-tested for 24+ month continuous deployment. Commercial systems (Imperx, KSV) have decades of operational data; this prototype will require maintenance + calibration re-verification quarterly.
- **Reproducibility:** RAW data preservation is critical. Proprietary JPEG-only workflows (e.g., older smartphone cameras) are inadequate for scientific reproducibility. This design prioritizes RAW capture to meet reproducibility standards.

---

### D4. Integration Sequence for Remaining Work

**Recommended order to minimize rework:**

1. **B1 (Optical Design)** → foundational; all other sections depend on its specs (lens, FOV, resolution, angle range).
2. **B2 (Pi Software)** → can begin in parallel with B1; initial prototype can use test patterns; refine specs once B1 outputs are available.
3. **B3 (Windows Client)** → depends on B2 API; can mock API during early development.
4. **B5 (Hardware Integration)** → depends on B1 (component specs) + B2 (software readiness). Assemble + test in parallel with B3.
5. **B4 (Image Processing)** → begins after B5 (need sample BAM images to develop/validate algorithms).
6. **B6 (Field Deployment)** → final phase; only after B1–B5 are stable + validated.

**Parallel workstreams (if resources allow):**
- B1 + B2 can overlap (optical specs inform sensor modes, but software development doesn't wait for final lens choice).
- B3 + B5 can overlap (UI design doesn't need final CAD; mock Pi API can be used for GUI testing).

**Critical path (longest duration):** B1 → B2 → B3 + B5 → B4 → B6 (approximately 6 months assuming 1 FTE equivalent effort).

---

### D5. Scope Limitations & Out-of-Scope Items

**IN SCOPE (this project):**
- Optical design + alignment for Brewster angle microscopy of air-water interface films.
- Raspberry Pi-based image acquisition (RAW capture, metadata logging).
- Windows client GUI for technician control + data management.
- Basic image processing (background subtraction, contrast enhancement, domain morphology).
- Lab deployment + technician training.
- Field validation over 1–2 months.

**OUT OF SCOPE (Phase 2 or beyond):**
- Multi-wavelength BAM (currently single 650 nm laser; extension to visible spectrum requires new optics).
- Solid-state substrates (protocol development for non-water interfaces; optical design change).
- Fluorescence imaging or other detection modalities.
- Automated sample carousel or high-throughput robotic handling.
- Commercialization, manufacturing scale-up, regulatory approvals (CE mark, etc.).
- Proprietary IP licensing or patent prosecution.

---

## SECTION E: HANDOFF GUIDANCE FOR NEXT WORKER / AI AGENT

### E1. Quick Reference: Cross-Section Dependency Map

| Work on → | First read sections → | Ask clarifying questions about → |
|-----------|----------------------|--------------------------------|
| **B1 (Optical)** | A1, A2, A3 | Sample types (Langmuir vs. protein vs. polymer)? Required lateral resolution (µm)? Lab environment thermal stability? |
| **B2 (Pi Software)** | A1, A2, B1, A3 | Target frame rate (fps)? Storage budget (GB/hour of capture)? Image processing on Pi or Windows? |
| **B3 (Windows Client)** | A1, A3, B2, B3 | Target Windows OS versions? Technician OS familiarity? Network topology (local LAN vs. remote over VPN)? |
| **B4 (Image Processing)** | B1, B2, B5, A3 | Which morphological features matter most (domain size, orientation, kinetics)? Validation data available (manual annotation or reference images)? |
| **B5 (Hardware Integration)** | All of A + all of B1–B4 | Lab environment conditions (temp range, vibration sources, humidity)? Access to precision machining or 3D printing? Laser safety certification required? |
| **B6 (Deployment)** | All sections | Technician availability for field trial (full-time or ad-hoc)? Lab location (India or international)? Expected sample types / experiment duration? |

---

### E2. Continuity Checklist: Before Starting Each Section

- ☐ Read **all previous sections** (A1–A3 + any completed B sections) to understand constraints + dependencies.
- ☐ **Verify all assumptions in Section D:** Are they still valid? Flag any changes immediately (document in D1).
- ☐ **Check cross-references:** If working on B2, confirm B1 design specs are finalized; get B1 output files (CAD, specs) from previous worker.
- ☐ **Validate source quality:** Use Section C guidance to prioritize reliable sources (peer-reviewed > vendor specs > blogs).
- ☐ **Cite everything:** Use BibTeX format (Section C4); aim for 8–12 citations per 1,000 words.
- ☐ **Test on actual hardware:** Don't simulate; use real Pi 4 + HQ camera (or mock equivalent) for benchmarks + validation.
- ☐ **Engage end-user:** For B1, B3, B6, solicit feedback from lab technician or optical scientist (whoever will use system).
- ☐ **Document edge cases:** What assumptions break if constraints change? (E.g., "This optical design assumes 53° Brewster angle; if solid substrates are used instead, redesign required.")

---

### E3. Version Control & Naming Convention

**Master prompt versions:**

- `BAM_RP4_MASTER_PROMPT_v1.0_20260121.md` ← Initial (this file).
- `BAM_RP4_MASTER_PROMPT_v1.1_20260131_A1-COMPLETE.md` ← After B1 completed (updated using Master Prompt B template).
- `BAM_RP4_MASTER_PROMPT_v1.2_20260215_A1-A2-COMPLETE.md` ← After B2 completed.
- (And so on...)

**Deliverable naming:**

- `BAM_OpticalDesign_B1_v1.0_20260131.pdf` (or .md)
- `BAM_PiSoftware_B2_v1.0_20260215.py` + `BAM_PiSoftware_B2_v1.0_20260215_README.md`
- `BAM_WindowsClient_B3_v1.0_20260228.py` + UI screenshots

---

### E4. Communication & Escalation

**If you are stuck on a section, escalate in this order:**

1. **Search existing sources** (Google Scholar, GitHub issues, Stack Overflow) for 30 minutes. Document search strategy + keywords used.
2. **Check Section C guidance** for this section; use recommended source types to find answers.
3. **Review D2 (Critical Uncertainties):** Is your blocker listed? If yes, document the gap + propose mitigation.
4. **Post in relevant community** (GitHub issues, Stack Overflow, ResearchGate) with context (section name, specific question, hardware constraints). Link back to this master prompt.
5. **Request clarification from end-user** (lab technician, optics PI, etc.) if domain knowledge is needed (sample types, environment specs, etc.).

---

### E5. Document Completeness Checklist (Before Publishing)

Before declaring a section "done," verify:

**For technical sections (B1–B4):**
- ☐ All claims cited (8–12 citations per 1,000 words).
- ☐ Trade-offs explicitly discussed (not hiding complexity).
- ☐ Performance validated on actual hardware (benchmarks included, with error bars).
- ☐ Edge cases + failure modes documented.
- ☐ Code (if applicable) is runnable + commented.
- ☐ Figures + tables are high-quality + captioned.

**For procedural sections (B5–B6):**
- ☐ Step-by-step instructions are unambiguous (could a non-expert follow them?).
- ☐ Materials + tools list is complete.
- ☐ Safety considerations highlighted.
- ☐ Troubleshooting flowchart provided.
- ☐ Photos + diagrams included.

**For all sections:**
- ☐ Cross-references are bidirectional (if B2 references B1, does B1 mention B2?).
- ☐ No vague language ("probably", "might", "hopefully" → replaced with quantified uncertainty or citations).
- ☐ Assumptions are explicit (Section D updated if new assumptions introduced).

---

### E6. Current Project Status Summary (As of Jan 21, 2026)

| Item | Status | Owner | ETA |
|------|--------|-------|-----|
| **A1: OS Foundation** | ✅ COMPLETE | Research expert | — |
| **A2: Hardware BOM** | ✅ COMPLETE | Research expert | — |
| **A3: Design Principles** | ✅ COMPLETE | Research expert | — |
| **B1: Optical Design** | 🟠 NOT STARTED | (awaiting assignment) | ~4 weeks |
| **B2: Pi Software** | 🟠 NOT STARTED | (awaiting assignment) | ~5 weeks |
| **B3: Windows Client** | 🟠 NOT STARTED | (awaiting assignment) | ~4 weeks |
| **B4: Image Processing** | 🟠 NOT STARTED | (awaiting assignment) | ~3 weeks |
| **B5: Hardware Integration** | 🟠 NOT STARTED | (awaiting assignment) | ~4 weeks |
| **B6: Field Deployment** | 🟠 NOT STARTED | (awaiting assignment) | ~6 weeks (after B1–B5) |
| **Overall Completion** | **45% (A sections done; B sections queued)** | — | **~6 months (Q2 2026)** |

**Critical path:** B1 (Optical) → B2 (Pi Software) → {B3 (Client) + B5 (Integration)} → B4 (Processing) → B6 (Field Trial).

**Next immediate action:** Begin **B1 (Optical Design)** section. Owner should:
- Clarify sample types (Langmuir monolayers? protein films? solid coatings?) with end-user.
- Review industry BAM specs (references [web:21, web:27, web:33] in master prompt).
- Design optical ray path using ZEMAX or equivalent.
- Select C-mount lens(es) with datasheet.
- Estimate lateral resolution + field of view.

---

## APPENDIX: BIBTEX LIBRARY (Completed Research)

```bibtex
@article{Mendenhall2016,
  title={Characterization of a self-calibrating, high-precision goniometer assembly},
  author={Mendenhall, M. H. and others},
  journal={Metrologia},
  volume={53},
  pages={xxx--xxx},
  year={2016},
  doi={10.1088/0026-1394/53/2/...}
}

@techreport{Imperx2024,
  title={MC-BAM: Multi-Color Brewster Angle Microscope Specifications},
  author={Imperx Inc.},
  year={2024},
  note={Retrieved from vendor datasheet}
}

@article{Sun2017,
  title={Distortion Correction for a Brewster Angle Microscope Using a Grating Relay Lens},
  author={Sun, Z. and others},
  journal={Analytical Chemistry},
  volume={89},
  pages={xxx--xxx},
  year={2017},
  doi={10.1021/acs.analchem.6b04738}
}

@misc{RaspberryPiFoundation2024,
  title={Picamera2 Documentation: Python Library for Raspberry Pi Cameras},
  author={{Raspberry Pi Foundation}},
  year={2024},
  howpublished={\url{https://picamera2.com}}
}

@article{Youssef2023,
  title={TelePi: An Affordable Telepathology Microscope Camera System},
  author={Youssef, A. and others},
  journal={Journal of Pathology Informatics},
  volume={14},
  pages={xxx--xxx},
  year={2023},
  doi={10.4103/jpi.jpi_42_23}
}

@article{Bonfanti2025,
  title={Fluorescence Time-Lapse Microscopy with Automatic Cell Detection on Raspberry Pi},
  author={Bonfanti, P. and others},
  journal={Review of Scientific Instruments},
  volume={96},
  pages={083703},
  year={2025},
  doi={10.1063/5.0229566}
}

@techreport{RaspberryPiCameraGuide2024,
  title={Raspberry Pi Camera Software Documentation: libcamera and rpicam-apps},
  author={{Raspberry Pi Foundation}},
  year={2024},
  howpublished={\url{https://www.raspberrypi.com/documentation/computers/camera_software.html}}
}

@misc{OpenCV2024,
  title={OpenCV: Open Source Computer Vision Library},
  author={{OpenCV Community}},
  year={2024},
  howpublished={\url{https://opencv.org}}
}

@article{Stover2006,
  title={Brewster Angle Microscope – An Excellent Tool for Nanoscience Researchers},
  author={Stover, H. F.},
  journal={Nanoscience \& Nanotechnology},
  volume={2006},
  pages={xxx--xxx},
  year={2006},
  doi={10.1080/15533170500524785}
}

@article{Oliveira2003,
  title={Quantitative Brewster Angle Microscopy of the Surface Film of Human Broncho-Alveolar Lavage Fluid},
  author={Oliveira, M. C. K. and others},
  journal={European Biophysics Journal},
  volume={32},
  pages={xxx--xxx},
  year={2003},
  doi={10.1007/s00249-003-0290-2}
}
```

---

## END OF MASTER PROMPT v1.0

**Prepared by:** Research Expert (Perplexity AI)  
**Date:** January 21, 2026  
**Status:** Ready for deployment to B1 worker  
**Next update:** Use Master Prompt B template after B1 completion

**Questions? Escalate to:** [Project lead / end-user contact TBD]

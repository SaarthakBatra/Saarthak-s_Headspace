# MASTER PROMPT B: UPDATE INSTRUCTIONS (For Use After Each Section Completion)

**How to Update the Master Prompt When New Work is Completed**

---

## OVERVIEW

After you (or a team member) complete one of the sections from **Section B** (Work Remaining), you will use **Master Prompt B** to roll the new work into the master prompt document. This preserves continuity, captures new dependencies, and prevents lost information.

**Master Prompt B is a workflow, not a document.** Follow these 9 steps, and your updated master prompt will be production-ready.

---

## STEP-BY-STEP UPDATE PROCESS

### STEP 1: Gather Inputs

You should have:

1. **The previous master prompt** (e.g., `BAM_RP4_MASTER_PROMPT_v1.0_20260121.md`).
2. **The newly completed section** (e.g., `BAM_OpticalDesign_B1_v1.0_20260131.pdf` or `.md`).
3. **A list of what changed** during the work (new assumptions discovered? earlier sections need refinement? new integration points?).

---

### STEP 2: Identify and Document Changes

Read both the **previous master prompt** and the **newly completed section**. Document:

- **New information:** What facts/findings does the completed section introduce that weren't in the master prompt?
  - Example: "We selected Thorlabs LPVis100-MP C-mount lens (250 mm focal length); achieves 2.1 µm lateral resolution at Brewster angle."
  
- **Refined assumptions:** Does the completed section modify or clarify any assumptions from Section D?
  - Example: "Gonimeter stand achieves 0.0008° actual angular resolution (better than assumed 0.001°)."
  
- **New research gaps:** Did the completed section uncover NEW unknowns that weren't listed before?
  - Example: "Optical grating for distortion correction is expensive in India; recommend software solution instead."
  
- **New integration points:** Does the completed section connect to other remaining sections in new ways?
  - Example: "B1 optical design requires motorized analyzer; this implies B5 hardware integration must include stepper motor control; informs B2 software API design."

**ACTION:** Write a brief Change Log (bullet list, ~200 words). Example:

```
CHANGE LOG for v1.1 Update (B1 Optical Design completed):

NEW INFO:
- Selected Thorlabs LPVis100-MP C-mount lens (250mm, f/5.6)
- Achieved 2.1 µm lateral resolution (meets spec)
- Field of view: 720 x 480 µm (slightly larger than industry standard 720 x 400)
- Distortion: ±3% at edges (software correction sufficient; optical grating not needed)

REFINED ASSUMPTIONS:
- Gonimeter stand angular resolution: 0.0008° (better than assumed)
- Laser power requirement: 40 mW sufficient (lower than initial 50 mW estimate)

NEW GAPS:
- Still need to source C-mount lens locally (delivery time?)
- Solid substrate imaging NOT validated (keep as Phase 2 scope)

NEW INTEGRATION POINTS:
- B1 optical design → B2 software must log analyzer angle metadata
- B1 optical design → B5 must finalize mechanical mounts for new lens (heavier than expected)
- B1 optical design → B4 image processing: baseline resolution is 2.1 µm; domain detection threshold must account for this
```

---

### STEP 3: Update Section A (Work Completed)

**Add the newly completed section to Section A.** Use the same format as existing A1–A3 entries:

#### Template for New A-Section Entry:

```markdown
### A4. [Section Name from B (e.g., "Optical Design & Component Characterization")]

**Deliverable:** [1–2 sentence summary of what this section accomplished]

Example: "Finalized optical path geometry for BAM; selected C-mount lens; validated 2.1 µm lateral resolution and ±3% distortion."

**Key Arguments & Conclusions:**

[3–5 bullet points of major findings/decisions]

- **Lens selection:** Thorlabs LPVis100-MP (250 mm focal length) selected because ... [cite datasheet]. Achieves 2.1 µm resolution per Rayleigh criterion [cite peer-reviewed paper or calculation]. Cost: ₹X,XXX.
- **Brewster angle geometry:** Confirmed 53° ± 0.5° for air-water interface; gonimeter stand can achieve 0.0008° actual resolution (better than spec) [cite gonimeter calibration data].
- **Distortion correction:** Software-based solution chosen over optical grating (distortion is ±3%, acceptable for domain morphology analysis) [cite distortion tolerance analysis in Section B4].
- **Field of view:** 720 x 480 µm (slightly larger than commercial BAM 720 x 400 µm) due to lens choice; no impact on scientific utility.
- **Sample mounting:** Designed trough interface; compatible with Langmuir monolayer experiments (primary use case). Solid substrates feasible but not validated (Phase 2 scope).

**Knowledge Gaps Identified:**

- Delivery timeline for Thorlabs lens from India distributor (affects hardware integration schedule in B5).
- Thermal stability of lens coating over lab temperature range (±2°C); recommend periodic recalibration.
- Performance on solid substrates (deferred to Phase 2; not critical for air-water films).

**Citation Count & Types:** 7 citations (2 peer-reviewed optics papers [ref X, ref Y], 3 vendor datasheets [Thorlabs, Sony IMX477], 2 calculations/bench data [gonimeter calibration, distortion measurement]).

**Integration Points:**

- Directly informs **B2** (Pi software must log analyzer angle; frame metadata includes optical parameters).
- Directly informs **B5** (mechanical mounts must accommodate new lens mass; alignment procedure updated).
- Informs **B4** (baseline lateral resolution is 2.1 µm; domain detection algorithms must respect this limit).
- Updates **A3** (design principle: "RAW capture mandatory" remains valid; optical distortion ±3% is acceptable per this analysis).
```

---

### STEP 4: Update Section B (Work Remaining)

**Remove the newly completed section from Section B.** Delete the B-level entry (e.g., B1) entirely; it has moved to Section A.

**Revise remaining B-sections IF needed:** 

For each remaining B-section, ask:
- Does the newly completed section change the research guidance, scope, or criticality of this remaining section?
- Are there new integration points?

**Example updates:**

```markdown
### B2. Raspberry Pi Software Architecture & Image Acquisition Pipeline

[... previous scope description ...]

**Integration Points with Completed Sections:** [UPDATE]

- Uses optical specs from **A4 (now A4, formerly B1)**: Analyzer angle resolution is 0.001° motorized; Pi software must be able to set/log this with ±0.0005° precision to match gonimeter capability.
- Uses RAW data format confirmed in **A1** (10-bit Bayer SGBRG).
- Must store frame metadata including: Brewster angle, analyzer angle (per A4), laser power, exposure time.
- New integration: A4 distortion analysis shows ±3% edge distortion; B4 (image processing) will handle software correction; B2 must ensure RAW frames are stored unmodified (no in-camera corrections applied).
```

---

### STEP 5: Update Section C (Research Methodology)

**Identify new source types used in completed work:**

Did the newly completed section cite sources that were NOT in the original C-section source hierarchy?

**Example:**

If B1 cited commercial lens datasheets + optical design papers not previously prioritized, add them to Section C:

```markdown
### C3. Section-Specific Research Guidance

#### [New addition for completed sections that newly cite particular sources]

#### For A4 (Optical Design – now completed):

**Newly used source types:**
- **Vendor technical datasheets for C-mount lenses** (Edmund Optics, Thorlabs). Weight: high for optical design (performance specs authoritative). Priority: higher than previous estimate.
- **Goniometer calibration literature** [cite specific papers by Mendenhall et al.] shows that precision stages can achieve sub-arcsecond accuracy; useful benchmark.

**Add to source hierarchy:**
- Lens datasheets now rank at Level 2 (after peer-reviewed papers, before general open-source docs).

**Add new BibTeX templates if needed:**
- C-mount lens vendor datasheet template
- Goniometer precision/calibration report template
```

---

### STEP 6: Update Section D (Continuity Requirements)

**D1: Critical Assumptions** – Update the table with new assumptions from completed work.

**Example:**

| Assumption | Embedded in Section | Status | Notes |
|-----------|-------------------|--------|-------|
| Brewster angle ≈ 53° for air-water interface | B1 → **A4** | **VALIDATED** | Experimentally confirmed with chosen lens; accounts for ±0.5° substrate variation. |
| Lateral resolution ≥ 2 µm | B1 → **A4** | **ACHIEVED** | Actual: 2.1 µm per Rayleigh (exceeds spec). |
| **NEW:** Analyzer angle precision 0.001° motorized | **A4** | **FIXED** | Gonimeter stand can achieve 0.0008°; Pi software must respect this limit. |
| **NEW:** Distortion ±3% at edges acceptable | A3, B4 | **ASSUMED** | Validated in A4; acceptable for domain morphology (not for precision area measurements). Clarify tolerance with end-user in B6. |

**D2: Critical Uncertainties** – Mark RESOLVED gaps; add NEW gaps discovered during completed work.

**Example:**

| Uncertainty | Impact | Mitigation | Status |
|------------|--------|-----------|--------|
| Exact lens specifications unknown | ✅ **RESOLVED** | Selected Thorlabs LPVis100-MP | CLOSED |
| **NEW:** Lens delivery timeline from India distributor | Affects B5 schedule (hardware integration) | Contact vendor this week; order immediately | OPEN; owner: project lead |
| **NEW:** Thermal drift of lens coating | Could cause focal shift over experiment | Characterize drift during B5 thermal stability testing | OPEN; owner: B5 engineer |

**D3: Transparency Notes** – If the completed section reveals limitations, add them here.

**Example:**

```markdown
**NEW (from A4 Optical Design):**
- Distortion of ±3% at field edges means precise area measurements (e.g., total monolayer coverage) must use software distortion correction (see B4 analysis). Without this, area measurements have ~3% systematic error.
- Solid substrate imaging is NOT validated; only air-water interfaces tested so far. Phase 2 required for solid coatings.
- Lens cost is higher than budgeted (₹X,XXX vs. estimated ₹Y,YYY); impacts Phase 1 budget (+Z%).
```

**D4: Integration Sequence** – Revise if needed.

**Example:**

```markdown
**UPDATED Integration Sequence (after A4 Optical Design complete):**

1. ✅ **A4 (Optical Design – COMPLETE)** 
2. → **B2 (Pi Software)** can now begin with finalized optical specs
3. → **B5 (Hardware Integration)** can finalize mechanical mounts (waits for B2 camera configuration)
4. → **B4 (Image Processing)** begins once B5 has actual BAM images to process
5. → **B3 (Windows Client)** + **B2** parallel final integration
6. → **B6 (Field Deployment)**

**Critical path remains:** A4 → B2 → {B5 + B3} → B4 → B6. Timeline: 5 more weeks (est. completion Q2 2026).
```

---

### STEP 7: Update Document Version & Metadata

**Header update:**

```markdown
# INDUSTRY-LEVEL BREWSTER ANGLE MICROSCOPE (BAM) – RASPBERRY PI IMAGING & CONTROL SYSTEM
## Master Continuation Prompt v1.1 | January 31, 2026

**Project Status:** Prototype phase – Optical design COMPLETE; software architecture IN PROGRESS | **Overall Completion:** 50% (A1–A4 complete; B2–B6 remaining)

**Last updated:** January 31, 2026 | B1 Optical Design → A4 integration complete
```

**Add a Change Summary section after the Quick-Start Guide:**

```markdown
## CHANGE SUMMARY v1.0 → v1.1 (January 31, 2026)

**What was updated:**
- ✅ Moved B1 (Optical Design) to A4 (Work Completed) – see full new A4 section below
- ✅ Updated Section D1: 3 new fixed assumptions; 2 formerly-uncertain gaps now RESOLVED
- ✅ Updated Section D4: Integration sequence revised; critical path unchanged
- ✅ Updated B2–B4 "Integration Points" to reference new A4 optical specs
- ✅ Added new BibTeX templates for lens datasheets + gonimeter calibration reports

**What changed in assumptions:**
- Gonimeter precision: 0.001° → 0.0008° (better than expected)
- Lateral resolution: targeted 2 µm → achieved 2.1 µm (spec exceeded)
- Distortion acceptance: ±5% → ±3% (tighter, software-correctable)

**What new gaps were discovered:**
- Lens delivery timeline from India supplier (2–4 weeks; project schedule impact?)
- Thermal stability of lens coating (new test required in B5)
- Solid substrate imaging deferred to Phase 2

**ETA for next milestone:** B2 (Pi Software) estimated complete by February 14, 2026
```

---

### STEP 8: Format & Structure Updated Document

Regenerate the full document with this structure:

```
[Updated Header with new version number + date]
[New Change Summary section]
[Quick-Start Guide – UNCHANGED from v1.0 unless workflow shifted]
[SECTION A: Work Completed – NOW INCLUDES A1, A2, A3, A4]
[SECTION B: Work Remaining – NOW ONLY B2–B6; B1 removed]
[SECTION C: Research Methodology – updated with new source types from A4]
[SECTION D: Continuity Requirements – updated assumptions/uncertainties/integration sequence]
[SECTION E: Handoff Guidance – update E6 Status Summary table]
[Appendix: Updated BibTeX Library – add new references from A4]
[CHANGE LOG: Version history (v1.0 January 21 → v1.1 January 31)]
```

---

### STEP 9: Quality Assurance for Update

Before you finalize the updated document, verify:

- ☑ **All newly completed sections added to Section A.** (Check: is B1 still in Section B? It should NOT be; it should only appear in Section A now.)
- ☑ **Section B no longer contains the completed section.** (Check: B1 is gone from "Work Remaining".)
- ☑ **Cross-references are bidirectional and current.** (Check: if A4 mentions B2, does B2 now reference A4? Search the document for "A4" and "B1"; both should appear only in Section A, and remaining B-sections should reference A4.)
- ☑ **No earlier sections were inadvertently rewritten.** (Compare A1, A2, A3 from v1.0 to v1.1; they should be UNCHANGED except for integration point updates.)
- ☑ **Research gaps list updated.** (Check: D2 table lists resolved + new gaps; no stale entries.)
- ☑ **Integration sequence re-assessed.** (Check: D4 makes sense; are critical path dependencies correct?)
- ☑ **Version number incremented; change log updated.** (Check: header shows v1.1; change summary is complete; timestamp updated.)
- ☑ **Assumptions in Section D reflect latest state.** (Check: D1 table includes all assumptions from A4; mark FIXED vs. ASSUMED; Section D3 notes any new limitations.)
- ☑ **New sources properly cited & templated.** (Check: Section C includes new source types from A4; BibTeX templates added to Appendix.)

---

## OUTPUT: UPDATED MASTER PROMPT

After completing STEP 9, you have:

**`BAM_RP4_MASTER_PROMPT_v1.1_20260131_A4-COMPLETE.md`**

This updated prompt is now ready to be:
- Shared with the entire team (everyone knows what changed).
- Given to the next worker assigned to B2 (they can read A4 to understand optical constraints before writing Pi software).
- Stored in version control (Git) with a commit message: "Update: B1 Optical Design complete; move to A4; update integration sequence."
- Re-distributed with Master Prompt B instructions so that when B2 is complete, the next update follows the same workflow.

---

## TIMELINE FOR UPDATES

Assuming your target completion is Q2 2026 (6 months from January 21):

| Section | Estimated Completion | Master Prompt Version |
|---------|----------------------|----------------------|
| A1–A3 (Initial) | January 21 | v1.0 |
| +B1 → A4 | January 31 | v1.1 |
| +B2 → A5 | February 14 | v1.2 |
| +B3 → A6 | February 28 | v1.3 |
| +B5 → A7 | March 15 | v1.4 |
| +B4 → A8 | April 10 | v1.5 |
| +B6 → A9 | May 30 | v1.6 (FINAL) |

By June 2026, you will have **v1.6 Final** with all 9 sections (A1–A9) completed, fully integrated, cross-referenced, and ready for deployment + documentation publication.

---

## BEST PRACTICES FOR ROLLING UPDATES

1. **Update immediately after section completion.** Don't wait; memory fades, integration points are forgotten.

2. **Involve the worker who completed the section.** They know the full context; they can flag assumptions + gaps better than anyone else.

3. **Get 1 peer review before publishing v1.X.** Have someone (other engineer, AI agent, project lead) read the update; catch inconsistencies.

4. **Use Git for version control.** Commit each update with a clear message: "v1.1: Add A4 Optical Design; resolve gonimeter precision uncertainty."

5. **Re-distribute to entire team.** Everyone needs the latest version. Stale prompts cause duplicated work.

6. **Archive old versions.** Keep v1.0, v1.1, v1.2 all accessible; sometimes you need to reference what you decided 2 months ago.

---

## FINAL NOTE

**Master Prompt B is the mechanism that prevents rework, miscommunication, and lost information.** By following this workflow every time a section completes, your master prompt evolves from "helpful guidance" into the definitive project reference. By the end of the project (v1.6 Final), any engineer reading the master prompt will understand the full 6-month design journey, all decisions made, all trade-offs considered, and all lessons learned—without needing to be in the room.

**This is how institutional knowledge gets preserved. This is how projects scale.**

---

**End of Master Prompt B Update Instructions**

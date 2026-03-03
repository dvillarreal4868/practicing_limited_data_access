
===============================================================================
ILD-RETRO-2026-001: SYNTHETIC RESEARCH DATA REPOSITORY
Retrospective Chart Review - Smoking and Interstitial Lung Disease
===============================================================================

ALL DATA IN THIS REPOSITORY IS FICTIONAL AND FOR EDUCATIONAL/PRACTICE USE ONLY.

PURPOSE:
This repository simulates the file structure and data formats you would encounter
when managing data for a retrospective clinical research study at an academic
medical center. It is designed for practicing data management workflows.

DIRECTORY STRUCTURE:
--------------------
00_study_metadata/          Study protocol (JSON), data dictionary (CSV), IRB info
01_structured_ehr_exports/  Compiled CSVs exported from Epic Clarity/Caboodle
                            - demographics.csv (1 row per patient)
                            - smoking_history.csv (1 row per patient)
                            - encounters.csv (1 row per encounter, multiple per patient)
                            - lab_results.csv (1 row per lab result)
                            - medications.csv (1 row per medication order)
                            - vitals.csv (1 row per vital sign set)
                            - pulmonary_function_tests.csv (1 row per PFT session)
                            - billing_claims.csv (1 row per claim)

02_clinical_notes/          Individual .txt files organized by patient folder
                            (1 folder per patient, 1-3 notes each)
                            Formats: consult notes, follow-ups, ED notes, discharge summaries

03_pathology_reports/       Individual .txt files per biopsy case
                            Includes OCR artifacts from scanned outside records

04_imaging_dicom/           DICOM files organized per DICOM hierarchy:
                            Patient > Study > Series > Instance (.dcm)
                            - 2 series per patient (lung window + mediastinal)
                            - 5-8 synthetic slices per patient (real: 200-400)
                            - 512x512 pixel matrix with random noise data
                            - Valid DICOM headers with proper UIDs and metadata

05_imaging_reports/         Radiology reports as individual .txt files

06_redcap_export/           Simulated REDCap CSV export + data dictionary
                            (format matches REDCap's native export structure)

07_patient_messages/        MyChart message threads (.txt)

08_care_coordination/       Social work notes, scheduling logs, outreach documentation

09_outside_records/         Scanned/OCR'd documents from external facilities
                            (intentionally degraded quality to simulate real faxes)

10_quality_log/             Data quality issues log (CSV) + abstraction audit trail (JSON)

11_exports/                 Full dataset export (JSON) + SAS transport placeholder

FILE FORMAT NOTES:
------------------
- Structured data: CSV (compiled, all patients in one file per data type)
  This is how EHR bulk exports typically arrive from Clarity/Caboodle SQL queries.

- Clinical notes: Individual .txt files, one per note, organized by patient folder.
  In a real EHR, these would be extracted via a notes extraction tool or API.
  Each note is a separate document in the EHR.

- DICOM: Standard medical imaging format. Each .dcm file = one image slice.
  Organized hierarchically: Patient > Study > Series > Instance.
  Real HRCT studies contain 200-400 slices; this repo has 5-8 per patient for practice.

- Pathology: Individual text reports, one per case.

- REDCap: The CSV export format matches what REDCap generates natively.
  Includes a data dictionary CSV that defines all variables.

- Outside records: Deliberately degraded text to simulate OCR of scanned faxes.

REALISTIC FILE SIZES (this synthetic repo vs real):
---------------------------------------------------
  File Type              This Repo        Real Study (10 pts)
  Demographics CSV       ~2 KB            ~2-5 KB
  Encounters CSV         ~4 KB            ~10-50 KB
  Lab results CSV        ~4 KB            ~50-500 KB
  Clinical notes (all)   ~30 KB           ~500 KB - 5 MB
  DICOM (all patients)   ~40 MB           ~2-10 GB
  Single DICOM slice     ~524 KB          ~500 KB (comparable!)
  Pathology reports      ~8 KB            ~20-50 KB
  REDCap export          ~3 KB            ~5-20 KB
  Full repository        ~41 MB           ~3-12 GB

KNOWN LIMITATIONS OF THIS SYNTHETIC DATA:
------------------------------------------
1. DICOM files contain random noise, not anatomical images
2. Slice count is reduced (5-8 vs 200-400 per study)
3. No .sas7bdat / .xpt binary files (placeholder only)
4. No actual PDF documents (text placeholders)
5. No HL7/FHIR message formats (would appear in real integrations)
6. No audit logs from EHR access tracking (HIPAA requirement in real studies)

SUGGESTED PRACTICE EXERCISES:
------------------------------
1. Parse all CSVs into a unified relational database (SQLite/PostgreSQL)
2. Write a script to extract patient IDs from unstructured notes (.txt files)
3. Build a DICOM metadata reader that catalogs all imaging studies
4. Reconcile the REDCap export against the raw EHR CSVs for discrepancies
5. Create a data quality dashboard from the quality log
6. Write NLP scripts to extract smoking pack-years from free-text notes
7. Build an ETL pipeline that normalizes the messy race/ethnicity values
8. Generate a CONSORT-style flow diagram from the audit trail JSON
9. Practice de-identification verification across all file types
10. Create a master linking log between study IDs and file locations

===============================================================================

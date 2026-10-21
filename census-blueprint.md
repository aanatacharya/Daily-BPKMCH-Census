# Daily Hospital Census: Blueprint

## Files
| File | Purpose |
|---|---|
| `census-template.census.json` | The data file. Copy it each day and edit the numbers. |
| `census-viewer.html` | Opens a data file, lets you edit it, prints it, saves it back. |

**Naming convention:** `census-YYYY-MM-DD.census.json` (BS date, e.g. `census-2083-04-02.census.json`).

## Daily workflow
1. Open `census-viewer.html` in a browser.
2. Click **Load day** and pick yesterday's file (or the template).
3. Click **New day** (zeros every number, keeps the structure), then type the date.
4. Enter today's numbers. Totals and vacant beds calculate themselves.
5. Click **Save day** (downloads `census-<date>.census.json`), then **Print / PDF** for upload.
6. Copy the Nepali post text from the box at the bottom for Facebook.

## Field reference
Only enter the values marked **ENTER**. Everything marked *auto* is calculated and is never stored in the file.

### `meta`
| Field | Type | Notes |
|---|---|---|
| `hospital` | text | English name, shown in the header |
| `hospital_ne` | text | Nepali name, used in the post text |
| `date_bs` | text `YYYY/MM/DD` | **ENTER** each day |

### `summary` (top cards)
| Field | Type | |
|---|---|---|
| `admissions` | number | **ENTER** |
| `discharges` | number | **ENTER** |
| `new_diagnosed` | number | **ENTER** new diagnosed cancer patients |
| `day_care` | `[a, b]` | **ENTER** the two parts, e.g. `[32, 3]`; card shows the sum 35 *(auto)* |

### `bipanna_sewa` (all numbers, **ENTER**)
`Ministry of Health`, `Bagmati Province`, `Gandaki Province`, `Health Insurance`

### `services` (groups of `"Service name": count`, **ENTER**)
Groups: `Radiology`, `Surgery`, `Pathology`, `Radiotherapy`, `Operation Theatre`, `ECG`, `ECHO`.
Radiology: `USG`, `CT-SCAN`, `MRI`, `X-RAY`, `Mammogram`, `USG FNAC`, `USG Guided FNAC`, `CT Guided FNAC`.
Pathology: `Biochemistry`, `Hematology`, `Serology`, `Immunoserology`, `IHC`, `Microbiology`, `LBC`, `FNAC`, `Biopsy`, `Flowcytometry`, `Cytology`.
Radiotherapy: `3D-CRT`, `Brachytherapy`, `Cobalt`, `Planning`, `Countering`, `IMRT`, `LINAC`, `Simulation`, `VMAT`, `VC Treatment`.
Operation Theatre: `Major`, `Minor`, `Intermediate`, `Dressing`, `Thyridectomy`, `Suture out`.
ECG: `ECG`. ECHO: `ECHO`.
To add a service, add a new `"Name": 0` line inside its group. It appears automatically.

### `opd` (list, one row per department)
| Field | Type | |
|---|---|---|
| `dept` | text | fixed name |
| `new`, `old`, `ehs` | number | **ENTER** |
| row total | | *auto* = new + old + ehs |
| column totals | | *auto* |

### `inpatient` (list, one row per ward)
| Field | Type | |
|---|---|---|
| `ward` | text | fixed name |
| `beds` | number | **ENTER** (changes rarely) |
| `admit` | number | **ENTER** current admitted patients |
| `mortality` | number | **ENTER** |
| vacant | | *auto* = beds − admit (never below 0) |

## Rules
- Numbers only, no quotes, no commas (`47`, not `"47"`).
- Do not rename `schema` or the section names. The viewer needs them.
- Keep one file per day; never overwrite old days.



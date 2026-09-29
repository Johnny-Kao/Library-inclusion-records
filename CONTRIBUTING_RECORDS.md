# Library Inclusion Records — Contribution SOP

This document defines the standard workflow for adding or updating institutional inclusion records in this repository.

Its purpose is to make each update reproducible across sessions and operators without relying on private context, personal information, or prior conversation history.

## 1. Scope

Use this SOP when adding evidence that a library, archive, university, academic institution, or comparable organization has:

- accepted a publication;
- added a publication to a collection;
- created a catalogue or discovery record;
- added a publication to an institutional resource or access page;
- made an electronic publication available through an institutional platform;
- otherwise taken a verifiable institutional action concerning a specific publication.

Do not interpret inclusion as endorsement, affiliation, peer review, or recommendation unless the evidence explicitly establishes that fact.

## 2. Operating principle

Record only claims that are directly supported by available evidence.

If information is missing, ambiguous, inconsistent, or cannot be verified, ask for clarification before writing the record.

Do not infer or invent:

- dates;
- institutional status;
- acquisition route;
- donation status;
- author identity;
- ISBN, DOI, catalogue numbers, or other identifiers;
- publication metadata;
- archive timestamps;
- evidence-file provenance.

It is better to leave a field absent than to record an unsupported value.

## 3. Start of every new task

First inspect the current repository state before making changes.

Use GitHub MCP as the primary interface for:

- reading the repository;
- checking existing records;
- reading `README.md`;
- creating or updating text files;
- committing text changes;
- verifying the final repository state.

Do not assume that a local working copy exists.

Do not assume that evidence files are stored in any particular local folder.

If local files are required, ask the user for their current location.

Example:

> Where are the evidence files for this record stored?

A folder used in a previous task, such as `Book29`, must never be assumed to apply to a new task.

## 4. Minimum information required

Before creating a record, establish the following where applicable:

| Field | Requirement |
| --- | --- |
| Institution | Official institution name |
| Publication | Exact title |
| Institutional action | What the institution actually did |
| Date | Date of the institutional action or record |
| Public evidence | Official catalogue, platform, resource, or institutional URL |
| Identifiers | ISBN, DOI, URN, catalogue number, record ID, etc., if available |
| Publication metadata | Author, publisher, year, format, language, subjects, etc., when supported |
| Evidence files | Whether local PDF, WACZ, screenshot, HTML, or other evidence exists |

If one of these is necessary to support the intended claim and is unavailable, ask the user rather than filling it by inference.

## 5. Evidence hierarchy

Prefer evidence in roughly this order:

1. official persistent institutional record;
2. official catalogue or institutional platform page;
3. official institutional resource page;
4. independent archival copy such as the Internet Archive;
5. repository-preserved WACZ, PDF, HTML, screenshot, or equivalent capture;
6. private institutional correspondence retained by the author.

Private correspondence may support a record but must not be uploaded unless the user explicitly requests publication and confirms that doing so is appropriate.

Private email addresses, personal phone numbers, signatures, account information, correspondence screenshots, and other personal or non-public information must not be placed in this repository.

## 6. Claim classification

Use precise language.

Examples:

**Catalogue inclusion**

> Catalogued by [institution].

**Collection inclusion**

> Added to the collection of [institution].

**Institutional resource inclusion**

> Added to [institution]'s official resource page.

**Electronic lending/platform inclusion**

> Included in [institution]'s eBook platform and available for borrowing.

**Accepted digital donation**

Use only when the institution explicitly confirms acceptance of the work as a donation.

**Acknowledged donation**

Use when receipt has been confirmed but catalogue or collection inclusion has not yet been established.

Do not upgrade one status into another without evidence.

For example:

- platform listing ≠ accepted donation;
- email receipt ≠ catalogue inclusion;
- catalogue record ≠ institutional endorsement.

## 7. Repository structure

Standard record structure:

```text
records/
  <institution-slug>/
    <YYYY-MM-DD>/
      record.md
      metadata.json
      evidence/
        ...
```

When multiple distinct publications from the same institution are recorded on the same date, use a stable publication-specific subdirectory when necessary to avoid collisions.

Example:

```text
records/
  national-library-of-public-information/
    2026-09-29/
      61388/
      61389/
      61390/
```

Prefer a stable institutional record ID when one exists.

Otherwise use a short, filesystem-safe publication slug.

## 8. File and directory naming

All newly proposed filenames and directory names must be valid on both macOS and Windows.

Use only portable names.

Avoid:

```text
< > : " / \ | ? *
```

Do not use trailing spaces or trailing periods.

Prefer lowercase ASCII names with hyphens.

Recommended evidence filenames:

```text
platform-capture.wacz
platform-record.pdf
catalogue-capture.wacz
catalogue-record.pdf
page-snapshot.pdf
screenshot.png
capture-manifest.json
```

If the user will upload files manually, specify the exact destination directory and exact filenames before they upload.

Example:

```text
records/example-library/2026-10-01/12345/evidence/
  platform-capture.wacz
  platform-record.pdf
```

Do not rename or relocate user files without either performing the operation explicitly or telling the user exactly what filenames and destination paths are required.

## 9. Evidence-file workflow

Evidence files are optional unless needed to make the public record durable or independently verifiable.

Possible scenarios:

### No local files

Create the record using verified public sources only.

Do not fabricate placeholder evidence files.

### Local files exist

Ask for the exact local folder unless the user has already provided it in the current task.

Inspect the files before upload.

Verify at minimum:

- file type;
- source URL where determinable;
- capture timestamp where determinable;
- SHA-256 checksum;
- whether the content corresponds to the intended institutional record.

### User will upload manually

Do not attempt local-file access.

Provide:

- exact repository destination;
- exact portable filenames;
- which files are required;
- what each file should contain.

Continue the record once the user confirms that the files are present.

## 10. Tool preference

Use GitHub MCP whenever the required operation is supported.

Typical GitHub MCP work includes:

- repository inspection;
- reading existing files;
- creating `record.md`;
- creating `metadata.json`;
- creating `capture-manifest.json`;
- updating `README.md`;
- committing text changes;
- verifying committed files.

Use a local-machine tool only when required for operations GitHub MCP cannot reasonably perform, such as:

- reading local files;
- computing hashes for local files;
- inspecting WACZ contents;
- moving or renaming local files;
- uploading binary files from the local machine.

Do not use local-machine access merely because it is available.

## 11. `record.md`

`record.md` is the human-readable canonical explanation of the institutional action.

Include only relevant sections.

Typical structure:

```text
# Institution — Record Type

Record date
Institution
Publication
Author
Identifiers
Format

## Status

## Public bibliographic record

## Holdings / availability
(if applicable)

## Public evidence

## Archived evidence
(if applicable)

## Institutional confirmation
(if applicable)

## Evidence classification

## Preservation

## Scope
```

The `Status` section should be concise and should state only the strongest claim supported by the evidence.

The `Scope` section should prevent overinterpretation where useful.

## 12. `metadata.json`

`metadata.json` should contain structured facts corresponding to the human-readable record.

Common groups include:

```text
record_date
institution
publication
identifiers
platform_record / catalogue_record
holdings / lending_at_capture
evidence
public_sources
```

Do not force every existing schema field into every record.

The metadata should describe the evidence actually available for that record.

## 13. `capture-manifest.json`

Create a manifest when repository-preserved evidence files exist.

Record, where available:

```text
source_url
capture_date
capture timestamp
filename
repository path
SHA-256
capture software
record ID
key facts visible in the archived page
```

A manifest must describe the actual uploaded file, not an expected or planned file.

Do not mark:

```json
"preserved_in_repository": true
```

until the file is actually present in the repository.

## 14. README index

Every completed public record should normally be represented in the `Current records` table.

Required columns:

```text
Date
Institution
Publication
Status
Public evidence
```

The README entry is an index, not the full evidence record.

Keep the `Status` concise.

`Public evidence` should normally link to:

- the strongest official live source;
- important external archival source if available;
- repository-preserved evidence when useful;
- the corresponding `record.md`.

## 15. Transactional or changing data

Some public pages contain values that change over time, such as:

- number of available copies;
- borrowing status;
- holdings;
- platform availability;
- usage counts.

When recording such values, label them explicitly as capture-time facts.

Example:

> 2 of 3 copies available at the time of capture.

Do not present transient values as permanent institutional facts.

## 16. Update sequence

For a normal addition:

```text
Inspect repository
→ verify supplied public URLs
→ identify missing information
→ ask user only for genuinely missing information
→ inspect local evidence if applicable
→ compute hashes / capture metadata if applicable
→ prepare record.md
→ prepare metadata.json
→ prepare capture-manifest.json if applicable
→ update README
→ commit text files using GitHub MCP
→ upload binary evidence if applicable
→ verify final repository state using GitHub MCP
```

If binary evidence is expected but not yet available, do not falsely describe the record as fully preserved.

## 17. Final verification

Before declaring the task complete, verify:

```text
README entry exists
record.md exists
metadata.json exists
manifest exists if required
all referenced evidence files exist
all relative links resolve to the intended paths
public URLs correspond to the intended publication
identifiers match the source
SHA-256 values match the uploaded files
Status does not overstate the evidence
no private or personal information was accidentally committed
```

If any check fails, correct it before reporting completion.

## 18. Existing records

Do not silently rewrite historical records merely to make them conform to newer conventions.

When updating an existing record:

- preserve the factual history;
- distinguish new evidence from the original record date;
- avoid changing previously correct claims without reason;
- use Git history to maintain traceability.

## 19. Privacy rule

This repository is public.

Never commit personal or non-public information merely because it appears in source material or correspondence.

Exclude unless explicitly necessary and approved:

```text
personal email addresses
phone numbers
signatures
home addresses
account IDs
login information
private correspondence
identity documents
personal metadata unrelated to the institutional record
```

Public professional bibliographic information appearing on an official institutional record may be recorded when relevant.

## 20. Default behavior when uncertain

Do not guess.

Ask the user for the missing fact or evidence.

If the available evidence supports a weaker claim than the requested wording, use the weaker factual wording and explain the limitation before committing if it materially changes the record.

Accuracy and evidentiary traceability take priority over completeness.

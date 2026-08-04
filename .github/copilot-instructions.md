## Copilot instructions for NetApp Workload Factory release notes documentation

### Repository overview
Product: NetApp Workload Factory

NetApp Workload Factory is a cloud-based platform that provides specialized workload services running on Amazon FSx for NetApp ONTAP and other AWS infrastructure. This repository contains the internal release notes site that documents recent changes across all Workload Factory services.

### Repository structure
- `_whatsnew/` – Individual AsciiDoc release note entry files, named `YYYY-MM-DD_workload-name.adoc`, one file per workload per release date
- `_include/` – AsciiDoc include files that define the section heading for each workload (e.g., `=== Amazon FSx for NetApp ONTAP`); included immediately before each `_whatsnew/` file in the main page
- `_index.yml` – Landing page configuration for the release notes site
- `project.yml` – Site-level settings including the list of source repositories for auto-generated release notes, sidebar navigation, and product family reference
- `media/` – Images and other media assets

### Product-specific context

**Architecture and components:**
- Workload Factory is organized into discrete *workloads*, each representing a distinct cloud service area
- The release notes aggregate entries from multiple source repositories, one per workload, listed under `release_notes_autogen.repositories_features` in `project.yml`
- Each workload has its own heading include file in `_include/` and one or more dated entry files in `_whatsnew/`
- The `whats-new.adoc` page is manually maintained: each release date section uses `include::_include/workload-name.adoc[]` for the heading followed by `include::_whatsnew/YYYY-MM-DD_workload-name.adoc[leveloffset=+1]` for the content

**Key concepts:**
- *Workload* – A named service category within Workload Factory; current workloads are FSx for ONTAP, Databases, VMware, GenAI, EDA, and Setup and administration
- *FSx for ONTAP* – Amazon FSx for NetApp ONTAP; the primary storage backend for most Workload Factory services
- *EDA* – Electronic Design Automation workload; focuses on latency analysis and monitoring for EDA environments running on FSx for ONTAP
- *EVS* – Elastic VMware Service; referenced in VMware workload release notes in the context of TCO/savings calculators
- *GovCloud* – AWS GovCloud (US) regions; noted in release entries when a feature or service gains GovCloud support

**Naming conventions and terminology:**
- The product is always referred to as *NetApp Workload Factory* (full name) or *Workload Factory* (short form); not "WLF" or other abbreviations
- Workload section headings follow the patterns used in `_include/`: `Amazon FSx for NetApp ONTAP`, `Database workloads`, `VMware workloads`, `GenAI workloads`, `EDA workloads`, `Setup and administration`
- `_whatsnew/` file names follow the pattern `YYYY-MM-DD_workload-name.adoc` where *workload-name* matches the repository name suffix (e.g., `workload-fsx-ontap`, `workload-databases`, `workload-vmware`, `workload-genai`, `workload-eda`, `workload-setup-admin`)
- Links within `_whatsnew/` files use absolute URLs to `docs.netapp.com`

### Typical user workflows

**Add a new release entry:**
Create dated file in `_whatsnew/` → Write feature sections using level-3 headings (`===`) → Add `include::` lines in `whats-new.adoc` under the correct date heading (heading include first, then content include with `leveloffset=+1`)

**Add a new workload:**
Add workload heading file to `_include/` → Add workload repository to `release_notes_autogen.repositories_features` in `project.yml` → Create first `_whatsnew/` entry file → Add `include::` directives to `whats-new.adoc`

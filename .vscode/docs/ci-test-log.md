# CI/Workflow Test Log & Failure Tracking

## Objective

Document all CI workflow failures, root causes, and fixes as we encounter them during the phase-1 development cycle.

---

## Failures Encountered & Fixes

### 1. GitHub Actions html5validator Action Issue

- **Status**: FIXED ✓
- **Date**: 16 May 2026
- **Failure**: `Unable to resolve action 'Cyb3r-Jak3/html5validator-action@v7'`
- **Root Cause**: Action repository no longer exists or version was incorrect.
- **Fix Applied**:
  - Tried v0.4.2 (failed: version not found)
  - Tried v1.1.5 (failed: repository is not a GitHub Action, missing action.yml)
  - **Solution**: Install html5validator as Python package and run via `pip install` + `html5validator` command
- **Commit**: "Fix: run html5validator using Python in CI workflow"
- **Next Test**: Verify Python-based validation runs successfully in CI

### 2. HTML Partial Files Validation Error

- **Status**: FIXED ✓
- **Date**: 16 May 2026
- **Failure**: `html5validator` reported missing DOCTYPE, html, head, body tags in header.html and sidebar.html
- **Root Cause**: These are HTML partial fragments meant to be included in other pages, not standalone documents
- **Fix Applied**: Updated workflow to exclude these partials: `html5validator --root . --ignore header.html sidebar.html`
- **Commit**: "Fix: ignore HTML partial files in validation"
- **Next Test**: Verify html5validator passes with ignored partials

### 3. Content Updates - Featured Topics Expansion
- **Status**: COMPLETED ✓
- **Date**: 16 May 2026
- **Update**: Enhanced sidebar.html with expanded featured topics
  - Kept original articles: "Algorithms & Optimization" and "Machine Learning" with links to generic.html
  - Added new topics: "Unix & Linux", "Cloud & Architecture", "Code Snippets"
  - All featured topics now have proper hrefs linking to relevant knowledge base sections
  - Increased featured topics from 3 to 5 for better visibility
- **Commit**: "Update: expand featured topics with algorithms, ML, and new sections"
- **Note**: Provides better navigation to all knowledge base resources

### 4. Created Dedicated Knowledge Base Pages
- **Status**: COMPLETED ✓
- **Date**: 16 May 2026
- **New Pages Created**:
  - `algorithms.html` - Algorithms & Optimization guide with sorting, graphs, DP, search topics
  - `machine-learning.html` - Machine Learning & AI guide with supervised, unsupervised, neural networks, LLMs
  - `cloud-architecture.html` - Cloud & Architecture guide with AWS, containers, microservices, DevOps
- **Updates to sidebar.html**:
  - Removed default `generic.html` links
  - Linked featured topics to their dedicated pages:
    - Algorithms → algorithms.html
    - Machine Learning → machine-learning.html
    - Cloud & Architecture → cloud-architecture.html
  - Changed "Explore More" button to link to index.html (homepage)
- **Commit**: "Add: dedicated knowledge base pages (algorithms, ML, cloud) and update sidebar links"
- **Note**: Each page includes relevant subtopics and best practices for each domain

---

## Upcoming Tests

- [ ] Verify html5validator runs without errors after ignoring partials
- [ ] Check if remaining HTML files pass validation
- [ ] Test auto-merge workflow (once branch protection is set up on GitHub)
- [ ] Verify PR template displays correctly

---

## Notes

- Keep this log updated as new issues arise during CI runs
- Document both failures and successful test runs for reference
- Cross-reference commit hashes for traceability

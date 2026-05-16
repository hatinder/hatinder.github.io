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

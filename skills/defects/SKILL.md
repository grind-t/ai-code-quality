---
name: defects
description: Code quality defects.
disable-model-invocation: true
---

# Code quality defects

Describe each defect by these fields:

- `defect_description`: a short statement of the problem.
- `defect_location`: where the defect lives in the project.
- `defect_type`: a reference (as defined in the `toolkit:context-principles`
  skill) to the family of problems this defect belongs to.
- `defect_characteristic`: the ISO/IEC 25010:2023 quality characteristic the
  defect impairs.
- `defect_subcharacteristic`: the ISO/IEC 25010:2023 quality subcharacteristic
  the defect impairs.
- `defect_risks`: the `most_likely` and the `worst_credible` risks of the
  defect as a risk source per ISO 31000:2018, as in the consequence/likelihood
  analysis of IEC 31010:2019. Omit `worst_credible` when it matches
  `most_likely`. Each risk has:
  - `event`: a credible event, where every step follows from the defect
    rather than from another independent mistake, and no existing test,
    check or monitoring catches it before `consequence`.
  - `consequence`: the end effect per FMEA (IEC 60812:2018), with the defect
    as the failure cause, taken at the level of the product's users and
    owners. If the defect breaks nothing at run time, trace it through how
    fast and how reliably maintainers can work with the system.
  - `likelihood`: the ISO 31000:2018 likelihood of `consequence`: High,
    Medium or Low.
  - `severity`: the IEEE 1044-2009 Severity of `consequence`: Blocking,
    Critical, Major, Minor or Inconsequential.

Example:

```yaml
defect_description: Order totals are computed in three places
defect_location: src/orders/totals.py, src/billing/invoice.py, src/reports/sales.py
defect_type: Duplicated Code (Fowler, Refactoring, 2nd ed.)
defect_characteristic: Maintainability
defect_subcharacteristic: Modifiability
defect_risks:
  most_likely:
    event: A maintainer changes how totals are computed
    consequence: Each change takes three edits and three reviews, so changes to totals ship slower
    likelihood: High
    severity: Minor
  worst_credible:
    event: A maintainer changes totals and misses one of the three copies, and no test compares totals across them
    consequence: Customers are invoiced amounts that differ from their orders, and invoices have to be corrected and reissued
    likelihood: Medium
    severity: Critical
```

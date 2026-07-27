# Personal Loans Automation

## Business Problem

Manual regression testing of a multi-step loan application workflow is slow and error-prone to repeat by hand every release. Automating the end-to-end flow - form fill, submission, validation - turns a repetitive manual task into a repeatable, reliable check.

## Solution Overview

A Selenium WebDriver suite that automates the personal loan application journey end-to-end: filling the application form, driving it through each step, and asserting the expected outcomes. Test data is externalised to Excel via OpenPyXL rather than hardcoded, so scenarios can be added without touching the automation code. Screenshots are captured at key steps to make failures easy to diagnose.

## Architecture

```
Excel test data (OpenPyXL)
    |
Selenium WebDriver  --  drives the loan application UI end-to-end
    |
Assertions + screenshot capture  -->  test report
```

## Technologies Used

- Python
- Selenium WebDriver
- OpenPyXL (Excel-based test data)

## Testing Concepts Demonstrated

- End-to-end UI flow automation across a multi-step form
- Data-driven testing (test data kept separate from test logic)
- Screenshot capture for failure diagnosis

## Key Learnings

- This was an early automation project, and the main lessons were foundational ones that carried forward into everything since: getting locator strategy and explicit waits right (rather than fixed sleeps), and structuring scripts so they stay maintainable as the suite grows.
- Externalising test data to Excel rather than hardcoding it made the suite far easier to extend with new scenarios later.

## Code

Private repo (`Ploans`) - kept private as it automates a specific application workflow rather than being a general-purpose tool.

## Future Enhancements

- Migrate to a page-object model for better maintainability as the suite grows
- Add CI integration for automatic regression runs

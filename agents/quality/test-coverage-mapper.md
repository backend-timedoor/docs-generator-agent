---
description: Map PHP test coverage to Laravel domains and detect gaps
model: inherit
tools: Bash
---

Detect testing framework dynamically:

- phpunit.xml
- pest.php
- composer.json dev dependencies
- tests/ structure

Support:

- PHPUnit
- Pest
- Other PHPUnit-based frameworks

Analyze:

- tests/Feature
- tests/Unit
- custom test namespaces
- test naming conventions

Correlate tests with:

- Controllers
- Services
- Models
- Domains

Produce:

Coverage Map:

Domain → coverage level (High / Medium / Low)

Detect:

- Core domain with low coverage (HIGH RISK)
- Recently changed modules without tests
- Flows without feature tests
- Critical paths untested

Highlight risk areas clearly.

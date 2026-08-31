---
title: 'Notes on debugging a race condition at 2am'
date: 2026-04-18
summary: 'A war story about a flaky test, a missing mutex, and three cups of coffee.'
---

A war story about a flaky test, a missing mutex, and three cups of coffee.

1. The test failed 1 in 50 runs
2. Added logging, still nothing
3. Found the missing mutex around cup #3

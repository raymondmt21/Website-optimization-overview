# Website Optimization Overview

**Chaos Unleashed** | Proprietary tooling (overview only; source code is private)

Tools and techniques for cutting Core Web Vitals on any website, plus the measurement
discipline to prove the gains are real. The techniques are page-agnostic and apply to any
site with a heavy front end; they were first built and proven on a content-heavy commercial
site, taking its mobile load time from roughly 21 seconds down to roughly 4 seconds.

## The problem

A slow site costs engagement, conversions, and search ranking, and the usual "fixes" often
just game the synthetic score without making the site genuinely faster for real users. The
brief here was explicit: improve *real-world* speed, not the number on a report.

## What this toolkit does

**Layered script deferral - the core technical insight.** Scripts that block a page's first
paint arrive by several different routes: some are discovered by the HTML parser, some are
injected dynamically after the page parses, and some are inserted by the platform in a spot
that server-side templating cannot reach. No single deferral technique catches all of them.
The toolkit intercepts blocking work at each of those distinct layers and restores it after
the page is usable, behind an idle gate with retry handling so nothing that was merely
delayed gets dropped.

**Protecting the measured element.** The browser picks one element as the "largest
contentful paint," and that measurement can be silently hijacked by a late-rendering overlay
(a cookie banner, for example). The toolkit ensures the intended main content is preloaded
and prioritized, and shields the measurement from being redefined by unrelated late content.

**Eliminating layout shift.** Above-the-fold space is reserved for asynchronously loaded
media so nothing jumps as the page assembles - driving cumulative layout shift to zero,
which is both a better experience and a better score.

**Measurement as a first-class deliverable.** A companion set of measurement scripts run the
before-and-after as a median of repeated runs under throttled network and CPU conditions.
This is deliberate: single runs are noisy and easy to cherry-pick, so every reported number
is a median under load. The same scripts make the result reproducible by anyone, rather than
a screenshot that has to be taken on faith.

## Results

Mobile load time (Largest Contentful Paint) dropped from roughly 21 seconds to roughly 4
seconds, with layout shift eliminated. Notably, the reporting also documented a regression
honestly rather than re-running until the numbers looked clean - because the point was real
speed, not a flattering screenshot.

## Why it matters

The through-line is intellectual honesty applied to performance work: fix the actual load
path, protect the real metric, and report the results (including the ugly parts) under a
reproducible method. That is what separates genuine optimization from score manipulation.

---
*Chaos Unleashed. This repository is a public overview. The implementation is proprietary
and maintained privately.*

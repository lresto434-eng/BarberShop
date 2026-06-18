# Booking Modal Design

**Date:** 2026-06-18
**Project:** Old Fashioned Barbershop — single-page static site

---

## Overview

Add a slide-in booking modal to the existing static HTML site. Clients fill in a short form; submissions are delivered to Savvas via email (Formspree) and optionally via WhatsApp. The "Book Now" button and hero CTA replace their current Fresha links with modal triggers.

---

## Architecture

- **Single file:** All changes live in `index.html`. No new files, no build step.
- **Email delivery:** Formspree free tier. Form `action` points to `https://formspree.io/f/{FORM_ID}`. The placeholder recipient is `angelresto25@icloud.com` — Savvas replaces it with his own email after creating a Formspree account.
- **WhatsApp:** `wa.me/306975922974` link with all booking details pre-filled as a URL-encoded message. No third-party service required.

---

## Form Fields

| Field | Type | Required |
|---|---|---|
| Name | Text input | Yes |
| Phone / WhatsApp | Tel input | Yes |
| Service | Dropdown (6 options with prices) | Yes |
| Preferred Day | Text input (e.g. "Friday") | Yes |
| Preferred Time | Text input (e.g. "Morning") | Yes |
| Message | Textarea | No |

Service dropdown options: Men's Haircut €12, Kids Haircut €8, Head Shave €15, Beard Trim €8, Hair & Beard €18, Hot Towel Shave €20.

---

## Submission Flow

1. Client fills the form and clicks **Send Booking Request**
2. Form POSTs to Formspree → email sent to `angelresto25@icloud.com` (placeholder)
3. On success: form content replaced with a confirmation message + **Book via WhatsApp** button
4. WhatsApp button opens `wa.me/306975922974` with a pre-filled message containing all submitted details
5. On error: inline error message shown, form stays intact

---

## Modal Behavior

- **Slide in from the right**, full viewport height
- **Triggers:** header "Book Now" button, hero "Book Your Appointment" CTA, nav "Book" link
- **Close:** ✕ button, click on dark overlay behind modal, Escape key
- **Mobile:** full-screen width on viewports ≤ 540px
- **Scroll lock:** `body` overflow hidden while modal is open

---

## Visual Design

Matches the existing site aesthetic:
- Background: `--dark-card` (`#1C1610`)
- Border: amber `--border`
- Labels: amber uppercase, 0.65rem, wide letter-spacing
- Inputs: `--dark-mid` background, amber focus border
- Submit button: full-width amber, same style as existing `.btn-book`
- WhatsApp button: transparent with green `#25D366` border and text
- Close button: small square, amber on hover

---

## Existing Site Changes

| Element | Before | After |
|---|---|---|
| Header "Book Now" | `href` → Fresha URL | `href="#"` + `onclick` opens modal |
| Hero CTA "Book Your Appointment" | `href` → Fresha URL | `href="#"` + `onclick` opens modal |
| Nav | No booking link | "Book" link added, triggers modal |
| Contact section "Book via Fresha" block | Links to Fresha | Replaced with a "Book Now" button triggering the modal |
| Services note | Links to Fresha | Fresha link kept here as fallback reference |

No sections are removed. All existing content, styles, and layout remain intact.

---

## Out of Scope

- No backend, no database, no user accounts
- No real-time availability / calendar integration
- No payment processing
- Formspree account setup is the client's responsibility (instructions to be provided in a comment in the HTML)

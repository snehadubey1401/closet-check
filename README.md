# Closet Check

**Know what you own before you buy.** Closet Check is a phone-first wardrobe app. Snap a piece of clothing (in a shop or from a Myntra screenshot) and see the similar pieces you already own, in seconds.

This is a Product Owner portfolio project. I took one idea through the full product journey: discovery, research, problem framing, user flows, screen design, and a working proof of concept.

**Live demo:** https://snehadubey1401.github.io/closet-check (open it on your phone)

---

## The problem

People who shop often lose track of what they own. They buy near-duplicates, forget pieces for months, and wear only a small part of their wardrobe.

Digital wardrobe apps already exist (Whering, Acloset, Indyx, Stylebook and others). They are built around outfit planning, and their biggest weakness is setup: users have to photograph their whole wardrobe before the app is useful, and most give up.

## My angle

Instead of "another digital closet", Closet Check is **a second opinion at the moment of buying**:

> Snap the item you are about to buy and see what similar pieces you already own, before you pay.

The wardrobe builds up one item at a time, each time you buy or wear something, so there is no big upload session.

## Discovery

I ran a short survey (Google Form shared on Instagram and WhatsApp) to test my assumptions. Early results from the first 6 responses:

| Assumption | Signal |
|---|---|
| Duplicate buying is common | 6 of 6 have bought something similar to what they owned; 4 "often" |
| People forget what they own | 4 of 6 "often" forget pieces; 4 of 6 wear less than 25% of their wardrobe |
| Nobody has a system today | 0 of 6 use any tracking app or method |
| The "check before buying" idea is wanted | Rated 5/5 by 4 people, 3/5 by 2 |
| People will photograph each item | **Only 2 of 6 would do it easily.** This is the main risk |

Full notes: [docs/discovery.md](docs/discovery.md)

**Key insight:** people love the outcome but will not do the work. Every design decision below responds to that.

## Design principles

1. **Add a piece in under 10 seconds.** One photo; the app detects the colour; the user taps the type.
2. **Search like you talk.** Type "black dress" or "work tops".
3. **One tap check before buying.** Works with a camera photo or a shopping-app screenshot.

## What the POC does

| Feature | How it works |
|---|---|
| Add a piece | Camera or gallery photo, auto-detected colour, one-tap type, optional occasion and price. A timer shows how many seconds it took. |
| Search and filter | Free-text search across name, type, colour and occasion, plus type filters |
| Check before buying | Scan an item, tap its type, see owned pieces ranked by % match. "Skip it" logs money saved; "Buy anyway" adds it in one tap. |
| Item details | Log "I wore this today", times worn, last worn, cost per wear, find similar pieces |
| Insights | % of wardrobe worn in 30 days, money saved, forgotten pieces (60+ days), colour mix |

The app opens with 8 example pieces so anyone can try it straight away.

## How it works (tech)

A single static page: HTML, CSS and plain JavaScript, no framework, no backend.

- **Colour detection** (`dominant()`): shrinks the photo to 64×64, estimates the background from the border pixels, ignores pixels close to it, and takes the most common remaining colour. `nearestColour()` maps it to a named colour using CIELAB distance, which matches how people perceive colour difference.
- **Similarity** (`similarity()`): 55% colour closeness (CIELAB distance) + 45% garment type (same type, related type such as top/kurta, or unrelated). 70% or more counts as "similar".
- **Storage**: IndexedDB in the browser. Photos are resized to 520px JPEGs. Data stays on the device; there is no account or server.
- **Routing**: URL hash (`#wardrobe`, `#check`, `#add`, `#insights`).

Run it locally by opening `index.html` in any browser.

## Known limitations (deliberate POC scope)

- Garment type is a manual tap, not image recognition.
- Matching uses colour and type only, not pattern, fabric or cut.
- Data lives on one device and does not sync.

## What I would do next

- **Validate behaviour, not opinions:** a one-week concierge test where people send a WhatsApp photo each time they buy or wear something.
- **Cut the effort further:** AI image tagging (type, pattern, sleeve length) and importing items from order-confirmation emails.
- **Measure:** duplicates skipped per user per month, items added per week, and week-4 retention.

## Product process

| Phase | Output |
|---|---|
| Discovery | Competitor scan, survey, assumption map |
| Define | Problem reframe: from "digital wardrobe" to "duplicate-purchase prevention" |
| Design | User flows and 9 mobile screens (Miro) |
| Build | This POC |
| Next | Concierge test, interviews, backlog for v2 |

---

Built by Sneha Dubey, Associate Product Owner.

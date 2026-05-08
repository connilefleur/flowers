# Visual Redesign — Tiny Cat Delivery Service

**Date:** 2026-05-08  
**Status:** Approved

## Goal

Replace the Game Boy pixel-art aesthetic with a naive folk-art flat illustration style, inspired by a hand-painted ceramic tile featuring a deadpan black cat. Retain all existing functional behaviour (three screens: start, delivery, delivered).

## Style Reference

Source: `Cat.jpeg` — a ceramic tile painting of a black cat eating ramen. Key visual properties:
- Flat solid color blocks, zero gradients, zero shading
- Bold black outlines on all elements
- Warm muted palette: dusty salmon pink, teal/blue, warm brown/tan, cream/white, black
- Naive childlike proportions: oversized round head, minimal body
- Deadpan expression (droopy white eyes, small pink nose)

## Layout

**Frameless, full-screen, two horizontal color bands:**
- Top band: dusty salmon pink `#E8867A`, ~45% viewport height
- Bottom band: warm tan/brown `#C4855A`, ~55% viewport height
- No card wrapper, no device shell, no border
- Content (cat, text, buttons) sits directly on the bands, centered
- Fully responsive — bands stay fixed; content scales/stacks naturally

## Color Palette

| Token | Hex | Use |
|---|---|---|
| Pink | `#E8867A` | Top background band |
| Brown | `#C4855A` | Bottom background band |
| Teal | `#4FA8C0` | Cat body/sweater, accent |
| Black | `#111111` | Cat, outlines, text, buttons |
| Cream | `#F5EFE0` | Button text, eye whites |
| Gold | `#F0B84B` | Flower petals, progress fill |
| Pink nose | `#E8A0A0` | Cat nose |

## Typography

- Font: **Nunito** (Google Fonts), weights 700 and 400
- All text: black `#111111`
- No pixel fonts

## Cat Character (SVG)

Inline SVG, not canvas. Reused across start and delivered screens.

- **Head**: large black ellipse, dominant proportion
- **Ears**: two small pointed black triangles
- **Eyes**: white circles with small dark oval pupils, positioned slightly low/droopy
- **Nose**: tiny pink triangle
- **Body**: small teal rounded rectangle below head (barely visible — head dominates)
- **Tail**: simple black curved path on right side

## Screens

### Start Screen
- Cat SVG centered in upper zone
- Title: "tiny cat delivery service" — large bold Nunito, black
- Subtitle: "1 flower · ready to send" — smaller, black
- Button: "send flower" — black background, cream text, bold Nunito, `3px 3px 0 #111` box-shadow offset (sticker feel), slightly rounded corners

### Delivery Screen
- **Track area**: full-width strip in the lower color band
- **Cat animation**: same SVG cat, 2-frame leg cycle (CSS class swap on interval), translates from off-screen left to center-right via `requestAnimationFrame` or CSS transition
- **Rainbow trail**: retained from original — 6 colored stripes (red → violet) drawn on a `<canvas>` behind the cat, extending from left edge to cat's current X position
- **Status text**: Nunito, black, centered below track
- **Progress bar**: black outline, cream background, fills with gold `#F0B84B`

### Delivered Screen
- "delivered :)" — large bold Nunito
- "for you" — medium Nunito
- **Flower SVG**: naive flat sunflower — 8 round petals in gold `#F0B84B`, black outline, dark brown center. Circular reveal animation (same radial clip logic as current), then gentle pulse (scale + slight rotation)
- Receipt text block: black border, cream background
- "send again" button — same style as start button

## Animation Details

- Cat walks at same speed as current (`SPEED = 0.82px/frame`)
- Leg cycle swaps every 6 frames (same `WALK_INT`)
- Rainbow trail canvas sits behind cat SVG element, same 6-stripe layout as current
- Delivery status messages and timing: unchanged from current `STEPS` array
- Flower reveal + pulse: same arc-clip reveal and sine-wave pulse as current, applied to SVG flower

## What Does NOT Change

- Three-screen flow and page transition logic
- Delivery timing, status messages, progress percentages
- Responsive scaling (fitToScreen logic, though applied to content rather than a device element)
- Rainbow trail colours and behaviour
- Flower reveal animation concept

## Future / Deferred

- OIIA OIIA spinning cat meme as alternative delivery animation (user requested deferral)

# Web Presentation Guide

This file explains how the presentation template works, how to edit it safely, how to decide what content belongs on each slide, and how to add animations later without breaking the layout.

## 1. What This Template Is

This presentation is a Reveal.js slide deck with:

- one loader file: `index.html`
- one shared visual theme: `css/theme.css`
- one HTML file per slide inside `slides/`
- optional logos inside `logos/`

The goal of this structure is:

- keep each slide isolated and easy to edit
- keep styling centralized
- make reordering simple
- support animations without adding a complex build system

## 2. How The Presentation Works

### Main Files

`index.html`

- loads Reveal.js from CDN
- defines the order of slides in the `SLIDES` array
- fetches each file from `slides/`
- initializes Reveal.js
- positions the slide number inside the slide frame

`css/theme.css`

- defines colors, fonts, spacing, and layout
- controls the style of headers, body text, figures, lists, and slide number
- contains responsive adjustments for smaller screens

`slides/*.html`

- each file contains exactly one slide
- each slide is a single `<section>` element
- this is where slide content should be edited most of the time

## 3. Basic Editing Workflow

### Edit Content

If you want to change the content of a slide:

1. open the matching file in `slides/`
2. edit the text, SVG, list, or layout inside that file
3. refresh the presentation in the browser

Examples:

- `slides/02_definition.html` for the definition slide
- `slides/07_exploration.html` for the exploration slide
- `slides/10_algorithm-examples.html` for references and examples

### Reorder Slides

If you want to change slide order, edit the `SLIDES` array in `index.html`.

Example:

```html
const SLIDES = [
  "01_title",
  "02_definition",
  "03_look-compute-move"
];
```

### Add A New Slide

1. create a new file in `slides/`, for example `15_future-work.html`
2. add one `<section>` block in that file
3. append the filename without `.html` to the `SLIDES` array in `index.html`

Minimal example:

```html
<section data-slide-id="future-work">
  <div class="slide-header">
    <div class="slide-title">6 - Future Work</div>
    <div class="slide-subtitle">A) Next Steps</div>
  </div>
  <div class="slide-body">
    <ul>
      <li>Extend to larger graphs</li>
      <li>Evaluate dynamic obstacles</li>
    </ul>
  </div>
</section>
```

## 4. Standard Slide Anatomy

Most slides follow this structure:

```html
<section data-slide-id="example-id">
  <div class="slide-header">
    <div class="slide-title">Section Name</div>
    <div class="slide-subtitle">Subsection Name</div>
  </div>
  <div class="slide-body">
    <!-- Content here -->
  </div>
</section>
```

### Meaning Of Each Part

`data-slide-id`

- unique identifier for the slide
- useful for URL hashes and future scripting

`.slide-header`

- top band of the slide
- contains the section title and subsection label

`.slide-title`

- major context for the slide
- should stay short and stable across a section

`.slide-subtitle`

- exact topic of the current slide
- should explain what changes from one slide to the next

`.slide-body`

- actual content area
- use it for text, SVG diagrams, lists, figures, and columns

## 5. Existing Layout Helpers

The CSS already provides reusable layout helpers.

### `.centered`

Use when the slide should visually center one main figure or one main concept.

### `.fig`

Use for an illustration plus caption.

### `.two-col`

Use for side-by-side comparison, diagram plus explanation, or problem vs solution.

### `.three-col`

Use for three-step processes or three concept blocks.

### `.r-stack`

Use for slide fragments where one visual state replaces another.

## 6. How To Decide Slide Content Correctly

This is the most important part for a good presentation.

### Core Rule

One slide should communicate one main idea.

If a slide tries to do too many things, the audience will remember none of them.

### Good Slide Content Usually Has

- one message
- one visual focus
- one title that says what the slide is about
- one subtitle that says what this specific step explains

### Avoid

- long paragraphs
- more than 4 to 5 bullets on one slide
- multiple unrelated diagrams on the same slide
- titles that are too generic, such as `Details` or `More`

### Practical Decision Rules

Use a text slide when:

- the main goal is definition, summary, or key takeaways

Use a diagram slide when:

- the audience needs to understand structure, topology, or a process

Use an animated slide when:

- the idea changes over time
- the explanation has steps
- a before/after comparison is important

Split one slide into two slides when:

- the diagram needs more than a few seconds to read
- you need to explain a concept first, then its example
- there is both definition and application in the same content block

## 7. A Good Header Strategy

For this deck, the header works best when:

- `.slide-title` contains the chapter or section
- `.slide-subtitle` contains the exact local topic

Examples:

- `1 - Luminous Robots` / `A) Definition`
- `2 - Problems` / `A) Exploration`
- `4 - Objective` / `C) Dynamic Environments`

This keeps navigation clear for the audience.

## 8. Animation Patterns Already Used In This Deck

This template already contains good examples of simple Reveal.js animation.

### Pattern 1: Fragment Swap

Used for slides where one state changes into another.

Example already present:

- `slides/07_exploration.html`
- `slides/08_gathering.html`

Pattern:

```html
<div class="r-stack">
  <svg class="fragment fade-out" data-fragment-index="0">...</svg>
  <svg class="fragment" data-fragment-index="0">...</svg>
</div>
```

What it does:

- the first visual is shown first
- when advancing, it fades out
- the second visual appears in the same place

Use this when you want to show progression without changing the full slide.

### Pattern 2: Simple Reveal Fragment

Use this when you want bullets or elements to appear step by step.

Example:

```html
<ul>
  <li class="fragment">First key idea</li>
  <li class="fragment">Second key idea</li>
  <li class="fragment">Third key idea</li>
</ul>
```

Use this for:

- staged explanations
- progressive disclosure
- keeping attention on one point at a time

### Pattern 3: Auto Animate

Reveal is initialized with `autoAnimate: true`.

This means you can create smoother transitions between similar slide states if:

- the next slide has similar structure
- related elements keep matching positions or attributes

Use this carefully. It is most useful when transitioning between:

- two versions of the same diagram
- a simplified state and an expanded state
- a first explanation and a refined explanation

## 9. Animation Design Rules

Animations should support understanding, not decoration.

Good animation:

- shows sequence
- highlights change
- reduces cognitive load

Bad animation:

- moves everything at once
- adds motion with no informational value
- makes the audience wait for unnecessary effects

### Recommended Practice

- animate only one concept at a time
- keep fragment count low
- prefer fade or replacement over flashy motion
- if an animation takes more than a few steps, split into multiple slides

## 10. How To Build Better Figures

This template already relies heavily on inline SVG, which is a strong choice.

Why inline SVG is good here:

- easy to edit directly in slide files
- sharp at any screen size
- easy to animate or duplicate
- no extra asset pipeline required

When making a new figure:

- use a consistent color palette
- label only what the audience needs to read
- remove visual noise
- prefer one diagram with emphasis over many small unrelated figures

## 11. Typography And Visual Roles

Current font roles:

- main content: `Inter`
- titles: `Space Grotesk`
- subtitles or supporting headings: `Outfit`

Use them consistently:

- titles for structure
- subtitle for local context
- body font for paragraphs and lists

This improves scanability and keeps the deck coherent.

## 12. Responsive And Screen Size Behavior

The deck uses a fixed design size through Reveal.js and is then scaled to the screen.

What this means:

- layout stays consistent across projectors and laptops
- content does not reflow unpredictably
- very dense slides may still become visually small on smaller screens

So when creating a slide, always prefer:

- less content
- larger visual focus
- stronger hierarchy

## 13. Local Preview

Because the deck loads slide files with `fetch()`, you should open it through a local server, not directly as a `file://` page.

Examples:

```bash
python3 -m http.server
```

or

```bash
npx serve .
```

Then open the served address in the browser.

## 14. Suggested Workflow For Creating A Strong New Slide

Use this order:

1. define the one main message of the slide
2. choose whether the slide should be text, diagram, comparison, or animation
3. write the header
4. write only the minimum content needed
5. add one figure or one clear visual structure
6. if the explanation has steps, add fragments or split into two slides
7. review the slide from the audience point of view: what should be remembered after 5 seconds?

## 15. Quick Quality Checklist

Before keeping a slide, ask:

- Is the main message obvious?
- Is the header specific enough?
- Is there one visual focus?
- Is the slide readable from far away?
- Can I remove anything without losing meaning?
- Would animation help understanding, or only add motion?

If the answer is unclear, simplify the slide.

## 16. Best Future Improvements

Later, this deck can be improved further by:

- unifying header enumeration style across all slides
- creating reusable slide variants such as `definition`, `problem`, `comparison`, and `result`
- adding small helper classes for callouts and theorem-like statements
- standardizing animation patterns so every animated slide follows the same logic

## 17. Summary

This template is already strong because it separates:

- structure in `index.html`
- design in `css/theme.css`
- content in `slides/*.html`

To keep it strong:

- edit one slide at a time
- keep each slide focused on one idea
- use animation only when it explains change
- prefer clarity over density

That is the safest path to a clean, persuasive, and reusable presentation.
# Illustration prompts (for OpenAI image generation)

Data figures in `figs/` are generated from the run ledger with matplotlib and
should stay that way (exact values). These prompts are for the *illustrative*
figures — architecture and concept diagrams — where a generated image adds
polish. Style keywords tuned for a minimal, technical, paper-grade look.

## 1. Architecture diagram (hybrid vs baseline)

> Clean minimal technical diagram on white background, academic paper style,
> flat vector look, no gradients, thin dark-gray outlines, muted blue and gray
> color palette. Two side-by-side vertical stacks of transformer blocks, 6
> blocks each. Left stack labeled "Transformer++": all six blocks identical,
> gray, labeled "attention + MLP". Right stack labeled "memory hybrid": blocks
> alternate between gray "sliding-window attention + MLP" and blue "gated
> delta-rule memory + MLP"; each blue block has a small side-arrow loop to a
> small matrix icon labeled "fast-weight state S_t" indicating write/read
> during the forward pass. Byte tokens enter at the bottom, logits exit at the
> top. Sans-serif labels, generous whitespace, no shadows, no 3D.

## 2. Concept: read-only attention vs writable memory

> Minimal two-panel conceptual illustration, white background, flat vector
> style, muted palette (gray left panel, blue right panel), thin outlines,
> paper-grade. Left panel "read-only attention": a model icon repeatedly
> looking back over a long strip of text tokens with many faint dashed arrows
> pointing backward — conveys re-reading everything on every step. Right panel
> "writable fast-weight memory": the same strip of tokens, but the model icon
> writes a compact note into a small notebook/matrix icon once, then reads the
> note going forward — few solid arrows. Small captions under each panel:
> "re-derives the rule at every token" and "stores the rule, then applies it".
> No text other than the captions and panel titles, no 3D, no shadows.

## 3. Optional cover motif (repo social preview)

> Abstract minimal banner, wide aspect ratio, white background: a row of small
> gray squares (attention layers) with every second square replaced by a blue
> square containing a tiny grid (memory matrix), one thin blue arrow flowing
> left to right through all squares. Extremely clean, flat, generous margins,
> looks like a NeurIPS paper figure, no text.

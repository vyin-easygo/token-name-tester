# Scale Families

When defining a scale, pick the family that fits the property. Each family has its own vocabulary and its own range; mixing families within a single scale is a smell.

## T-shirt sizes
**Vocabulary:** `xs`, `sm`, `md`, `lg`, `xl`, `2xl`, `3xl`
**Description:** Anchored on a default middle (`md`), steps extend in both directions. In practice the scale usually grows asymmetrically (more steps above `md` than below). Use this scale family when the property has a clear default and values move bigger or smaller from there.
**Use for:** spacing, sizing, radii, font sizes
**Typical range:** 3-7 steps

## Emphasis
**Vocabulary:** `subtle`, `default`, `bold`, `strong`
**Description:** Ordered by visual prominence, not physical size. Use this scale family when the question is "how loud is this?" rather than "how big is this?" Asymmetric — there's usually a default and the scale extends upward more than downward.
**Use for:** opacity, color saturation, shadow depth, typography weight
**Typical range:** 3-4 steps

## Physical descriptor
**Vocabulary:** `thin`, `regular`, `thick`
**Description:** Direct names for a physical attribute. Limited range — meaningful distinctions run out quickly.
**Use for:** border widths, stroke weights, divider thicknesses
**Typical range:** 3-5 steps

## Tempo
**Vocabulary:** `slow`, `medium`, `fast`, `instant`
**Description:** Time-based ordering. Pairs naturally with role-scoped scales — "fast" in one motion role isn't the same duration as "fast" in another.
**Use for:** durations, animation timings
**Typical range:** 3-5 steps

## Density
**Vocabulary:** `tight`, `normal`, `loose`
**Description:** How much room something takes. Three-step is the natural size; more than that and the distinctions stop being legible.
**Use for:** line-height, letter-spacing, layout density
**Typical range:** 3 steps

## Presence
**Vocabulary:** `none`, `subtle`, `default`, `bold`
**Description:** An emphasis scale with an explicit zero step. The `none` step is structurally different from the others — it's not "less of the thing," it's "the thing is absent." Use when the property meaningfully has an off state.
**Use for:** radius (`radius.none`), borders (`border.none`), shadows (`shadow.none`)
**Typical range:** 4-5 steps

## Numeric ordinal
**Vocabulary:** `1`, `2`, `3`, `4`, `5`
**Description:** Pure ordering, no semantic content. Reach for this when steps don't have meaningful names, or when you have more than ~7 steps and t-shirt sizes start feeling forced.
**Use for:** elevation, z-index layers, shadow depth
**Typical range:** 5+ steps

## Named anchors
**Vocabulary:** Domain-specific (`body`, `caption`, `display`; `card`, `popover`, `modal`)
**Description:** Bespoke names that describe the *use* of each step rather than its position on a scale. Not a scale in the conventional sense — more like role names that happen to be ordered. Used as the `role` slot in role-scoped scales.
**Use for:** typography roles, elevation roles, motion roles
**Typical range:** as many as the domain needs

## Cross-cutting rules

Most scales are 3-7 steps. Below 3, you don't have a scale — just two named values. Above 7, switch to numeric ordinal; t-shirt sizes break down (`3xl`, `4xl`, `5xl` are forgettable).

Mixing families within one scale is a smell, but sometimes necessary. A radius scale of `none`, `sm`, `md`, `lg`, `full` mixes three families (presence + t-shirt + special anchor). Acceptable, but the reader has to learn which step belongs to which family.

Some properties have multiple defensible families. Typography weight can be emphasis (`regular`, `bold`, `strong`) or numeric (`300`, `400`, `600`, `700`). Pick based on whether consumers should think semantically or pick a specific value.

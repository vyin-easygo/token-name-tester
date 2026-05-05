---
Ideas: Remove the .sub-property slots and have property be defined as `font-weight`
Concerns: Component tokens that just map to semantic tokens are going to blow out the number of tokens we have massively
---

# Token Naming Convention

## Scales

### Primitive Scales

**Grammar:** `scale-category(.sub-category).step`
**Slots:**
- `scale-category`: The kind of value (color, space, radius, font, shadow, duration, z)
- `sub-category (optional)`: The sub-category within the category (color: blue, gray; font: weight, size, family). Omitted for single-dimension categories
- `step`: The numeric position on the scale (4, 8, 100, 500)
**Description:** Primitive tokens frequently define scales (colour ramps, space, radius, duration, font-size, etc). This grammar helps define these in a consistent way.
**When to use:** Use this grammar whenever you need to define a primitive scale with a numeric step
**When to avoid:** Avoid this grammar if you need to define a scale with non-numeric steps (see Semantic - Property Scales)

**Examples:**
- `duration.200`
- `shadow.2`
- `space.4`
- `border.radius.8`
- `color.blue.500`
- `color.gray.900`
- `font.size.16`
- `font.weight.400`

### Semantic Property Scales

**Grammar:** `property(.sub-property).step`
**Slots:**
- `property`: the design property (radius, border, space, opacity, duration, etc)
- `sub-property (optional)`: the sub-property within the property (border: width, radius; font: weight, family, etc)
- `step`: semantic scale family (t-shirt: `sm`, `md`, `lg`; emphasis: `subtle`, `default`, `bold`; density: `tight`, `normal`, `loose`; etc)
**Description:** Unlike Primitive Scales (that use numeric `step` slot values), Semantic Property Scales use semantic `step` slot values. Each `(sub-)property`'s `step`s all map to positions on the same underlying Primitive Scale. `border.radius.none`, `border.radius.sm`, `border.radius.md` are all positions on the `radius` Primitive Scale.
**When to use:** Use this grammar whenever you need to apply a semantic scale family to a property
**When to avoid:** Avoid this grammar if you need to define a primitive scale with a numeric step (See Primitive - Scales)

**Examples:**
- `border.radius.none`
- `border.radius.sm`
- `border.radius.md`
- `border.width.thin`
- `border.width.thick`
- `space.sm`
- `opacity.subtle`
- `duration.fast`
- `font.weight.bold`
- `font.size.xl`

### Semantic Role-Scoped Property Scales

**Grammar:** `category.role.property(.sub-property).step`
**Slots:**
- `category`: the design domain (typography, spacing, etc)
- `role`: the role within the category (body/heading/caption for typography; inline/stack/inset for spacing, etc)
- `property`: the design property (radius, border, space, opacity, duration, etc)
- `sub-property (optional)`: the sub-property within the property (border: width, radius; font: weight, family, etc)
- `step`: semantic scale family (t-shirt: `sm`, `md`, `lg`; emphasis: `subtle`, `default`, `bold`; density: `tight`, `normal`, `loose`; etc)
**Description:** Property Scales work well because each `(sub-)property`'s `step` references the same scale. In practice though, you tend to need a different scale as soon as a property is paired to a particular role. Role-Scoped Property Scales handle this by introducing a `role` slot (grouped under a `category`) that lets the `(sub-)property`'s `step` reference a different scale. For example, `typography.body.font.size.sm` and `typography.heading.font.size.sm` share `property`, `sub-property` and `step` names but resolve to different values.
**When to use:** Use this grammar when the `(sub-)property`'s `step` needs to reference a different scale based on the `role`
**When to avoid:** Avoid this grammar if a `(sub-)property`'s `step` always references the same scale (See Semantic - Property Scales)

**Examples:**
- `typography.body.font.weight.strong`
- `typography.heading.font.size.lg`
- `spacing.stack.gap.md`

---

### Semantic Roles

**Grammar:** `role.intent(.emphasis)(.state)`
**Slots:**
- `role`: where the token applies (`bg`, `fg`, `border`, `outline`, `shadow`)
- `intent`: the semantic meaning being expressed (`default`, `muted`, `brand`, `neutral`, `success`, `warning`, `danger`, `info`, `focus`, plus `on-*` variants for `fg`)
- `emphasis (optional)`: visual weight within the role+intent (`subtle`, `bold`). Only present when `role`+`intent` has more than one `emphasis` level.
- `state (optional)`: interaction state (`hover`, `pressed`, `focus`, `disabled`, `selected`, `visited`). Omitted for the resting state.
**Description:** Where the scale grammars refer to _positions_ on a scale, the Semantic Roles grammer refer to _purposes_ (independent of which components use them); the `intent`, `emphasis`, and `state` slots carry semantic meaning rather than scale position.

Slots are optional from right to left, drop what you don't need.

A slot holding its default value is omitted.

**When to use:** Use this grammar for tokens that describe a purpose in the UI rather than a position on a scale.
**When to avoid:** Avoid this grammar if you're naming a position on a scale (See Semantic - Property Scales or Role-Scoped Property Scales).

**Examples:**
- `bg.default`
- `bg.brand.subtle`
- `bg.brand.bold.hover`
- `bg.danger.subtle`
- `fg.default`
- `fg.muted`
- `fg.danger`
- `fg.on-brand`
- `fg.on-emphasis`
- `border.default`
- `border.danger`
- `outline.focus`
- `shadow.default`

### Components

**Grammar:** `component(.variant)(.part).property(.state)`
**Slots:**
- `component`: the component name (`button`, `input`, `card`, `tooltip`, `tab`, `dialog`)
- `variant (optional)`: the component variant (`primary`, `secondary`, `ghost`, `danger`). Omitted when the component has no variants.
- `part (optional)`: the sub-element (`background`, `label`, `icon`, `border`, `arrow`, `header`, `footer`). Omitted when the component is atomic.
- `property`: the property being tokenized (`color`, `padding`, `size`, `radius`, `gap`)
- `state (optional)`: interaction state (`hover`, `pressed`, `focus`, `disabled`, `selected`). Omitted for the resting state.
**Description:** Components consume Semantic Roles tokens by default. A component token is created only when there's something component-specific to encode: a value that *differs* from what a Semantic Roles token would resolve to, or a value that has *no Semantic Roles equivalent* (component-specific dimensions, paddings, gaps). When a component token is created, it references a Semantic Roles token where one fits, or a Semantic Property Scale or Primitive where no semantic equivalent exists.
**When to use:** Use this grammar when a component needs a value that diverges from a Semantic Roles token, or needs a value that has no Semantic Roles equivalent (typically dimensions and layout measurements).
**When to avoid:** Avoid this grammar when a Semantic Roles token, Semantic Property Scale, or Primitive can be consumed directly without compromise. Component tokens that are simple aliases of semantic tokens don't earn their own existence.

**Examples:**
- `button.primary.background.color.hover`
- `button.primary.label.color`
- `button.ghost.border.color.focus`
- `card.padding.size`
- `card.header.padding.size`
- `tooltip.arrow.size`
- `input.border.color.danger`
- `tab.indicator.size`

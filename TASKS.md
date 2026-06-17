# Distributions widget - View Options

Reference: biolab/orange3#7298

## Goal

The Distributions widget already has the View Options (gear icon)
dialog, but unlike Line Plot, Bar Plot and Violin Plot it doesn't let
you set a custom plot title or custom axis titles. We're adding that.

Relevant file: `Orange/widgets/visualize/owdistributions.py`, the
`ParameterSetter` class around line 177. The shared logic for titles
and axis labels already exists in
`Orange/widgets/visualize/utils/customizableplot.py`, and
`owviolinplot.py` / `owbarplot.py` show the pattern to follow.

## Branches

- `feature/distribution-view-options` - integration branch, everything
  below gets merged here first
- `core/title-axis-customization` - Sofian - main feature
  implementation
- `tests/visual-settings-persistence` - DFU398 - tests
- `docs/readme-and-demo` - abdna94 - README and demo prep
- `bugfix/widget-polish` - manammg - secondary widget fix

## Task breakdown

### core/title-axis-customization (Sofian)

- Add a `title_item` property to `ParameterSetter`
  (`self.master.getPlotItem().titleLabel`)
- Add `TITLE_LABEL` to `LABELS_BOX` in `initial_settings` (font)
- Add `ANNOT_BOX` with custom text for the plot title and the x/y axis
  titles
- The widget currently sets axis labels automatically based on the
  selected variable - when the user leaves the custom field empty it
  should keep falling back to that auto label

### tests/visual-settings-persistence (DFU398)

- Extend `Orange/widgets/visualize/tests/test_owdistributions.py`
- Cover `set_visual_settings` for the new title and axis title options
- Check that `visual_settings` survives saving and reloading a
  workflow (.ows round trip)

### docs/readme-and-demo (abdna94)

- Document the new View Options entries in the README
- Before/after screenshots of the widget
- Short demo script for the live presentation on 18.06

### bugfix/widget-polish (manammg)

- Pick one small existing issue in a widget and fix it as a bonus,
  for example the scroll position issue in
  `Orange/widgets/data/owfeaturestatistics.py` or the resize issue in
  `Orange/widgets/data/owcreateclass.py`
- Open it as its own PR into the feature branch

## Workflow

Branch off `feature/distribution-view-options`, open PRs back into
it. Once everything's merged there, we open one PR from
`feature/distribution-view-options` into `master`.

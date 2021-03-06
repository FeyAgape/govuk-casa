# `casaGovukRadios()`

Extends the [`govukRadios()`](https://design-system.service.gov.uk/components/radios/) macro.

Custom parameters:

* `casaValue` - the value of the chosen radio button. This is a convenience for toggling the `checked` flag on the appropriate `item`, but you can also manually set `checked` on each item if you need to use more specific logic for determining checked state.
* `casaErrors` - form errors (just pass `formErrors`)

## Example usage

Basic example:

```nunjucks
{% from "casa/components/radios/macro.njk" import casaGovukRadios %}

{{ casaGovukRadios({
  name: 'myInput',
  casaValue: formData.myInput,
  casaErrors: formErrors,
  items: [{
    text: 'Yes',
    value: 'yes'
  }, {
    text: 'No',
    value: 'no'
  }]
}) }}
```

If you want one of the radio items to toggle the display of an element:

```nunjucks
{% from "casa/components/radios/macro.njk" import casaGovukRadios %}

{% set panel %}
  This panel will remain hidden until the "Yes" radio button is chosen
{% endset %}

{{ casaGovukRadios({
  name: 'myInput',
  casaValue: formData.myInput,
  casaErrors: formErrors,
  items: [{
    text: 'Yes',
    value: 'yes',
    conditional: {
      html: panel
    }
  }, {
    text: 'No',
    value: 'no'
  }]
}) }}
```

## Displaying errors

ref: https://design-system.service.gov.uk/components/error-summary/

The error summary link must set focus on the first radio in the group. Unless you have specified an explicit `id` for the first item in the list, this macro will explicitly set that `id` to `f-<name>`, e.g. `f-preferences` in order for links from the error summary to work as expected.

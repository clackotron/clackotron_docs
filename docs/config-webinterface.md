---
title: "Config: webinterface.json"
permalink: /docs/config-webinterface
parent: "Configuration"
nav_order: 3
---

# Configuration: `webinterface.json`
The `webinterface.json` file is loaded by the webinterface to configure what options and buttons are displayed to the user and what strings are used for displaying text.

The `webinterface.json` file can be edited on your computer and uploaded as part of the filesystem via PlatformIO or directly on the device by enabling the config mode and opening `http://clackotronip:8080/edit?file=webinterface`. When editing directly on the device, you must manually reboot the device after editing.

## File format
The `webinterface.json` file contains a JSON object with multiple keys:
* `name` - The title of the webinterface.
* `version` - The version that is displayed in the webinterface.
* `expert` - Whether or not to show the `Expert` Mode button that allows the user to enter a custom template from the webinterface.
* `modes` - An array of modes that are displayed as mode buttons on the webinterface.
* `string` - An map of strings that are used for displaying text on the webinterface.

### Mode format
Each entry in the `modes` array must be an object with the following properties:
* `mode` - A unique, internal identifier for the mode.
* `title` - The name of the mode as shown on the webinterface.
* `template` - The template that is applied in the background. (See [template docs](misc-templates.md)).
* `paramNames` - Optional. A list of names that is shown for text or number input fields generated by the temaplte. E.g. if the template contains a free text input `{t1:4}` the webinterface will display it as `{t1:4}` for the user, unless a custom name is given here.

## Default
```json
{
  "name": "Clackotron 2000",
  "version": "1.0.0",
  "expert": true,
  "modes": [
    {
      "mode": "text",
      "title": "Custom\nText",
      "template": "{t1:4}",
      "paramNames": [
        "Text"
      ]
    },
    {
      "mode": "time",
      "title": "Current\nTime",
      "template": "{hh}{mm}"
    },
    {
      "mode": "weekday",
      "title": "Current\nWeekday",
      "template": "{WD}{DD}"
    },
    {
      "mode": "date",
      "title": "Current\nDate",
      "template": "{DD}{MM}"
    },
    {
      "mode": "year",
      "title": "Current\nYear",
      "template": "{YYYY}"
    },
    {
      "mode": "off",
      "title": "Off",
      "template": ""
    }
  ],
  "strings": {
    "title-mode": "Mode",
    "title-options": "Options",
    "title-preview": "Preview",
    "expert-mode": "Expert mode",
    "expert-template": "Expert template",
    "save-button": "Save configuration",
    "save-failed": "Failed to save config",
    "copyright": "Rietliau Clackotron 2000",
    "day-names-short": [
      "SO",
      "MO",
      "DI",
      "MI",
      "DO",
      "FR",
      "SA"
    ],
    "day-names-long": [
      "SON",
      "MON",
      "DIE",
      "MIT",
      "DON",
      "FRE",
      "SAM"
    ]
  }
}
```

## Examples (of Modes)
### A mode that shows the static text HOME
```json
  "modes": [
    {
      "mode": "hometext",
      "title": "HOME",
      "template": "HOME",
    }
  ]
```

### A text input mode that allows 20 characters
```json
  "modes": [
    {
      "mode": "customtext",
      "title": "Custom\nText",
      "template": "{t1:20}",
      "paramNames": [
        "Custom Input name"
      ]
    }
  ]
```

### A mode with a template that shows the full date and time
```json
  "modes": [
    {
      "mode": "fulldate",
      "title": "Full\nDate",
      "template": "{WDD} {DD}.{MM}.{YYYY} {hh}.{mm}",
    }
  ]
```

For more details on the template syntax, check out the [template docs](misc-templates.md).

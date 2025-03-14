---
title: "Entities use device classes where possible"
related_rules:
  - has-entity-name
  - entity-translations
  - icon-translations
---
import RelatedRules from './_includes/related_rules.jsx'

## Reasoning

Device classes are a way to give context to an entity.
These are used by Home Assistant for various purposes like:
- Allowing the user to switch to another unit of measurement than what the device provides.
- They are used for voice control to ask questions like "What is the temperature in the living room?".
- They are used for exposing entities to cloud based ecosystems like Google Assistant and Amazon Alexa.
- They are used to adjust the representation in the Home Assistant UI.
- They can be used to set a default name of the entity to decrease the burden on our translators.

Because of these reasons, it is important to use device classes where possible.

## Example implementation

In the example below we have a temperature sensor that uses the device class `temperature`.
The name of this entity will be `My device temperature`.

`sensor.py`
```python {5} showLineNumbers
class MyTemperatureSensor(SensorEntity):
    """Representation of a sensor."""

    _attr_has_entity_name = True
    _attr_device_class = SensorDeviceClass.TEMPERATURE

    def __init__(self, device: Device) -> None:
        """Initialize the sensor."""
        self._attr_device_info = DeviceInfo(
            identifiers={(DOMAIN, device.id)},
            name="My device",
        )
```

## Additional resources

A list of available device classes can be found in the entity pages under the [entity](/docs/core/entity) page.
More information about entity naming can be found in the [entity](/docs/core/entity#has_entity_name-true-mandatory-for-new-integrations) documentation.

## Exceptions

There are no exceptions to this rule.

## Related rules

<RelatedRules relatedRules={frontMatter.related_rules}></RelatedRules>
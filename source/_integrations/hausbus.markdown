---
title: HausBus
description: Integrate HausBus controllers and devices with Home Assistant.
ha_category:
  - Hub
  - Cover
ha_iot_class: Local Push
ha_config_flow: true
ha_codeowners:
  - '@hausbus'
ha_domain: hausbus
ha_release: "2026.9"
ha_platforms:
  - cover
ha_integration_type: hub
---

The **HausBus** {% term integration %} lets you connect Home Assistant to controllers and devices from [HausBus](https://www.haus-bus.de/), a local building automation system. The integration communicates locally with the HausBus controller and automatically discovers supported devices on the bus.

Currently, the integration provides support for roller shutters (covers).

## Supported devices

The integration currently supports:

- Roller shutters (Cover entities)

Each shutter channel is exposed as a Home Assistant Cover entity.

Supported operations:

- Open cover
- Close cover
- Stop cover
- Set cover position

## Prerequisites

Before setting up the integration:

- A supported HausBus controller must be installed and running on the local network.
- The controller must be reachable from Home Assistant.
- At least one supported HausBus shutter channel must be configured on the controller.

## Configuration options

{% include integrations/config_flow.md %}

1. {% my config_flow_start domain=hausbus title="**Settings** > **Devices & services**" %}, then select **Add integration**, and search for **HausBus**.
2. Home Assistant searches your local network for a HausBus controller. This can take a moment.
3. If a controller is found, the integration is set up automatically and supported devices are added.
4. If no controller is found within the search period, you can retry the search.


## HausBus automation examples

### Automation: Close the shutters at sunset

This automation closes a shutter when the sun sets.

```yaml
automations:
  - alias: "Close shutters at sunset"
    triggers:
      - trigger: sun
        event: sunset
    actions:
      - action: cover.close_cover
        target:
          entity_id: cover.living_room_shutter
```

### Automation: Open the shutters at sunrise

This automation opens a shutter when the sun rises.

```yaml
automations:
  - alias: "Open shutters at sunrise"
    triggers:
      - trigger: sun
        event: sunrise
    actions:
      - action: cover.open_cover
        target:
          entity_id: cover.living_room_shutter
```


## Troubleshooting

If no devices are discovered:

- Verify that the HausBus controller is connected to the local network.
- Verify that Home Assistant can reach the controller.
- Verify that supported shutter channels are configured on the controller.
- Reload the integration from its page under {% my integrations title="**Settings** > **Devices & services**" %}.

For more information, visit the [HausBus website](https://www.haus-bus.de/).

## Removing the integration

This integration follows standard integration removal.

{% include integrations/remove_device_service.md %}

Removing the integration does not modify the configuration of the HausBus controller or connected HausBus devices.

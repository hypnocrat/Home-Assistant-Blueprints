# Motion-activated Light Blueprint and helpers

This repository contains multiple blueprints and other files.

**advanced_motion_automation.yaml** is he main blueprint for controlling your lights. It controls the lights.  

**Manual_overrides.yaml** provides functionality for setting up manual overrides, i.e. motion not toggling your lights if you controlled it manually. This is optional and can be configured per room or for your whole setup at once. 

**reset_overrides.yaml** is a very simple blueprint that will turn your manual overrides off at sunset and whenever Home Assistant restarts


It is based on this blueprint:
https://github.com/iainsmacleod/Home-Assistant-Blueprints


## Features of main blueprint

- Control lights based on motion detection from one or more sensors
- Optional custom brightness and color settings
- Disabling sensors (vacation mode, sleep mode...)
- Support for (external) manual overrides per light. 
- Sun position awareness with configurable offset (day/night conditions)
- Configurable wait time after motion stops

##

## Installation

You can add this blueprint to your Home Assistant instance by:

1. Going to **Settings** > **Automations & Scenes** > **Blueprints**
2. Click the **Import Blueprint** button
3. Paste the URL of this repository and click **Preview**
4. Click **Import Blueprint**

## Configuration Options

### Required Settings

- **Motion Sensors**: One or more motion sensors that will trigger the lights
- **Lights and Switches**: One or more lights to be controlled by the automation
- **Wait Time**: Duration to keep lights on after motion stops (default: 60 seconds)

### Optional Settings

- **Use Custom Brightness and Color**: Toggle to enable custom light settings
- **Brightness**: Light brightness level (0-255)
- **Color**: RGB color value for the lights
- **Manual Override Helper**: You can provide a binary sensor here to indicate whether the light(s) have been controlled manually by you. If so, the automation will not trigger
- **Disable sensors**: You can provide one or more binary sensors here that will prevent the automation from controlling your lights. Sleep mode, vacation mode...

### Conditional Controls

- **Sun Condition**: Option to activate only during day, night, or regardless of sun position
- **Sunrise Offset**: Time offset from sunrise in HH:MM format. Positive number, it will keep running after sunrise (default 1h)
- **Sunrise Offset**: Time offset from sunset in HH:MM format. Negative number, it will start running before sunset (default -1h)


## How It Works

1. When motion is detected, the blueprint checks all configured conditions
2. If conditions are met and no disabling sensors are on, lights turn on with either default or custom settings
3. When motion stops, the blueprint waits for the configured time
4. After the wait period, lights are turned off

## Advanced Functionality

The blueprint includes several advanced features:

- **Mode: restart** - Ensures the automation restarts if triggered again during execution
- **Multiple Condition Checks** - Evaluates entity states, sun position, and disabling sensors
- **Template Conditions** - Uses templating for flexible condition evaluation
- **Sun Position with Offset** - Allows fine-tuning of day/night detection

## Example Use Cases

- **Hallway Lighting**: Turn on hallway lights when motion is detected, but only at night
- **Bathroom Lights**: Activate with custom brightness based on time of day
- **Kitchen Under-cabinet Lighting**: Turn on when motion is detected but only if the main kitchen light is off
- **Outdoor Pathway Lights**: Activate only after sunset with a specific color and brightness

## Troubleshooting

If your automation isn't working as expected:

- Check that your motion sensors are correctly reporting motion
- Verify that any conditional entities have the expected states
- Ensure your sun offset format is correct (HH:MM)
- Check that blocking entities aren't preventing activation

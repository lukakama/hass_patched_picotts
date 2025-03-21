# Home Assistant Patched Pico TTS integraion

This is a patched version of the original Home Assistant Pico TTS integration that fixes https://github.com/home-assistant/core/issues/93456

## What has been patched

The patch changes how the message is passed to the `pico2wave` subprocess, moving from a command line argument to the stdin. 

The patch should be equally, if not more, secure compared to the original code (peer reviews are welcome).

**NOTE**: Changing the subprocess invocation to use an OS shell would also fix the issue, but it would then expose to shell injection security issues, so it is a no-go.

## Installation with HACS

1. Add this repository as custom repository in HACS as described in https://www.hacs.xyz/docs/faq/custom_repositories/, using the following values:
    * Repository: lukakama/hass_patched_picotts
    * Type: Integration
2. Install the add-on
3. Proceed with the configuration (see below)

## Installation without HACS

Just copy the content of `custom_components` into the `custom_components` directory of home assistant configuration home, and then proceed with the configuration (see below).


## Configuration
1. Add the `patched_picotts` platform to the TTS integration:
    ```yaml
    # Example configuration.yaml entry
    tts:
      - platform: patched_picotts
    ```
    Available configurations are the same of official Pico TTS integration: https://www.home-assistant.io/integrations/picotts/
2. Reboot Home Assistant
3. Use the `patched_picotts` in place of the official `picotts` one
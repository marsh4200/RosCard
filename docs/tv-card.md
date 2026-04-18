# TV Card

The TV card now supports per-button actions using these Home Assistant entity types:

- `media_player`
- `remote`
- `script`
- `select`
- `button`

## TV Types

- `apple_tv`
- `android_tv` (`Google TV / Android TV` in the editor)
- `kodi`

## Kodi Notes

For `kodi`, the editor exposes Kodi-specific input presets for `media_player` entities such as:

- navigation: `Input.Up`, `Input.Down`, `Input.Left`, `Input.Right`, `Input.Select`, `Input.Back`
- UI actions: `Input.Home`, `Input.ContextMenu`, `Input.Info`, `Input.ShowOSD`
- playback: `media_play`, `media_pause`, `media_stop`, `media_next_track`, `media_previous_track`
- fullscreen: `Input.ExecuteAction` with `fullscreen`

These are sent through Home Assistant as `kodi.call_method` where needed.

## Button Entity Support

If you assign a row to a `button` entity, the card sends:

```yaml
service: button.press
target:
  entity_id: button.your_button
```

No extra command value is required.

## Example

```yaml
type: custom:aiks-tv-card
tv_name: Lounge TV
tv_type: kodi
entities:
  - key: POWER_ON
    type: media_player
    entity_id: media_player.kodi_lounge
    value: turn_on
  - key: UP
    type: media_player
    entity_id: media_player.kodi_lounge
    value: kodi_call_method:Input.Up
  - key: MENU
    type: media_player
    entity_id: media_player.kodi_lounge
    value: kodi_call_method:Input.ContextMenu
  - key: PLAY
    type: button
    entity_id: button.start_movie_mode
    value: ""
```

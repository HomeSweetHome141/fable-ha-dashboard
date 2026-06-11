# Fable Dark — Home Assistant Theme & Dashboard

A warm-dark Home Assistant theme with gradient card surfaces, plus a ready-made
three-column overview dashboard (Solar & Battery, Security, Energy Income,
Tesla, Locations).

The theme is installable via **HACS**. The dashboard is a single YAML file you
paste once — after that it is fully editable in the Home Assistant UI.

## Prerequisites

Install these from HACS first (all are in the default store):

| Card | Why |
|---|---|
| [card-mod](https://github.com/thomasloven/lovelace-card-mod) | Applies the gradient styling to every card via the theme |
| [Mushroom](https://github.com/piitaya/lovelace-mushroom) | Entity, alarm, and person cards |
| [ApexCharts Card](https://github.com/RomRider/apexcharts-card) | The Energy Income 30-day bar chart |

## 1. Install the theme (via HACS)

1. HACS → three-dot menu → **Custom repositories**
2. Repository: `https://github.com/HomeSweetHome141/fable-ha-dashboard` · Type: **Theme**
3. Find **Fable Dark Theme** in HACS and download it
4. Add **both** of these to `configuration.yaml`:

```yaml
frontend:
  themes: !include_dir_merge_named themes
  extra_module_url:
    - /hacsfiles/lovelace-card-mod/card-mod.js
```

> **IMPORTANT — gradients will not appear without `extra_module_url`.**
> Installing card-mod from HACS only registers it as a Lovelace resource.
> Theme-level styling (`card-mod-card`) only works when card-mod is ALSO
> loaded as a frontend module, which is what the
> `extra_module_url` line does.

5. Restart Home Assistant, then pick **fable-dark** in your user profile
   (bottom-left avatar → Theme).
6. If you had the theme selected before a theme update, reload it via
   **Developer tools → YAML → Reload themes**, then re-select it.

## 2. Install the dashboard

1. **Settings → Dashboards → Add Dashboard → New dashboard from scratch**
2. Open it → pencil icon (edit) → three-dot menu → **Raw configuration editor**
3. Paste the contents of [`dashboard/overview.yaml`](dashboard/overview.yaml) and save

## 3. Relink your entities

All entities in the dashboard are placeholders. Because the dashboard uses the
native *sections* view, you can relink everything from the UI — open the
dashboard, click the pencil icon, then click any card and pick your entity
from the dropdown. No YAML editing needed.

Placeholder map:

| Placeholder entity | Replace with |
|---|---|
| `sensor.battery_state_of_charge` | Home battery state of charge (%) |
| `sensor.solar_pv_power` | Current PV/solar output (kW) |
| `sensor.grid_import_power` | Grid import power (kW) |
| `sensor.grid_export_power` | Grid export power (kW) |
| `sensor.daily_energy_income` | Daily net energy income ($) — needs long-term history |
| `alarm_control_panel.home_alarm` | Your alarm panel |
| `lock.front_door` / `lock.back_door` | Door locks |
| `cover.garage_door` | Garage door |
| `binary_sensor.motion_sensors` | Motion sensor (or a group) |
| `binary_sensor.tesla_sentry_mode` | Tesla sentry mode |
| `lock.tesla_doors` | Tesla door lock |
| `sensor.tesla_battery_level` | Tesla battery (%) |
| `sensor.tesla_interior_temperature` | Tesla cabin temperature |
| `person.mike` / `person.sarah` | Your person entities |

## Troubleshooting

- **Cards look flat / no gradients** → you are missing the
  `extra_module_url` line above. Add it, restart HA, and hard-refresh the
  browser (Ctrl+F5).
- **Theme not in the profile list** → check the theme file ended up in
  `config/themes/` and that `themes: !include_dir_merge_named themes` is
  present under `frontend:`, then restart.
- **Income chart empty** → the placeholder `sensor.daily_energy_income`
  needs to be replaced with a real sensor that has history.

## Notes

- The gradient card look comes from `card-mod-card` inside the theme — it
  applies a vertical surface gradient plus a translucent border to every card
  automatically. Individual cards (battery gauge, alarm panel, income chart)
  layer extra gradients on top via `card_mod`.
- The income chart colors bars green for profit and red for loss
  automatically via `color_threshold`.
# Fable Dark — Home Assistant Theme & Dashboard

A warm-dark Home Assistant theme with gradient card surfaces, plus a ready-made
three-column overview dashboard (Solar & Battery, Security, Energy Income,
Tesla, Locations).

The theme is installable via **HACS**. The dashboard is a single YAML file you
paste once — after that it is fully editable in the Home Assistant UI.

## Prerequisites

Install these from HACS first (all are in the default store):

| Card | Why |
|---|---|
| [card-mod](https://github.com/thomasloven/lovelace-card-mod) | Applies the gradient styling to every card via the theme |
| [Mushroom](https://github.com/piitaya/lovelace-mushroom) | Entity, alarm, and person cards |
| [ApexCharts Card](https://github.com/RomRider/apexcharts-card) | The Energy Income 30-day bar chart |

## 1. Install the theme (via HACS)

1. HACS → three-dot menu → **Custom repositories**
2. Repository: `https://github.com/HomeSweetHome141/fable-ha-dashboard` · Type: **Theme**
3. Find **Fable Dark Theme** in HACS and download it
4. Make sure `configuration.yaml` includes:

```yaml
frontend:
  themes: !include_dir_merge_named themes
```

5. Restart Home Assistant, then pick **fable-dark** in your user profile
   (bottom-left avatar → Theme).

## 2. Install the dashboard

1. **Settings → Dashboards → Add Dashboard → New dashboard from scratch**
2. Open it → pencil icon (edit) → three-dot menu → **Raw configuration editor**
3. Paste the contents of [`dashboard/overview.yaml`](dashboard/overview.yaml) and save

## 3. Relink your entities

All entities in the dashboard are placeholders. Because the dashboard uses the
native *sections* view, you can relink everything from the UI — open the
dashboard, click the pencil icon, then click any card and pick your entity
from the dropdown. No YAML editing needed.

Placeholder map:

| Placeholder entity | Replace with |
|---|---|
| `sensor.battery_state_of_charge` | Home battery state of charge (%) |
| `sensor.solar_pv_power` | Current PV/solar output (kW) |
| `sensor.grid_import_power` | Grid import power (kW) |
| `sensor.grid_export_power` | Grid export power (kW) |
| `sensor.daily_energy_income` | Daily net energy income ($) — needs long-term history |
| `alarm_control_panel.home_alarm` | Your alarm panel |
| `lock.front_door` / `lock.back_door` | Door locks |
| `cover.garage_door` | Garage door |
| `binary_sensor.motion_sensors` | Motion sensor (or a group) |
| `binary_sensor.tesla_sentry_mode` | Tesla sentry mode |
| `lock.tesla_doors` | Tesla door lock |
| `sensor.tesla_battery_level` | Tesla battery (%) |
| `sensor.tesla_interior_temperature` | Tesla cabin temperature |
| `person.mike` / `person.sarah` | Your person entities |

## Notes

- The gradient card look comes from `card-mod-card` inside the theme — it
  applies `linear-gradient(180deg, #1c1b19, #201f1d)` plus a translucent
  border to every card automatically. Individual cards (battery gauge, alarm
  panel, income chart) layer extra gradients on top via `card_mod`.
- The income chart colors bars green for profit and red for loss
  automatically via `color_threshold`.

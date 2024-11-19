# HAMR-Tablette
**Voici le partage de mon travail réalisé avec beaucoup d'aide venant de la communauté et de temps. MERCI !**

_C'est une base qui trouvera ça forme définitive fin 2025_
## Home
![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/01.jpg)

<details>
  <summary>Sidebar-card</summary>

```yaml
sidebar:
  title: null
  clock: false
  digitalClock: true
  digitalClockWithSeconds: false
  twelveHourVersion: false
  period: false
  date: true
  hideTopMenu: true
  hideHassSidebar: true
  showTopMenuOnMobile: false
  dateformat: dddd, DD MMMM YYYY
  width:
    desktop: 7
    mobile: 0
    tablet: 7
  breakpoints:
    mobile: 768
    tablet: 1024
  sidebarMenu:
    - action: navigate
      active: true
      icon: mdi:home-assistant
      navigation_path: /tablette-a8/home
    - action: navigate
      active: true
      icon: mdi:home-thermometer
      navigation_path: /tablette-a8/temperature
    - action: navigate
      active: true
      icon: mdi:music
      navigation_path: /tablette-a8/media
    - action: navigate
      active: true
      icon: mdi:calendar
      navigation_path: /tablette-a8/calendrier
    - action: navigate
      active: true
      icon: mdi:map
      navigation_path: /tablette-a8/carte
    - action: navigate
      active: true
      icon: mdi:clipboard-list
      navigation_path: /tablette-a8/liste-de-taches
    - action: navigate
      active: true
      icon: mdi:cogs
      navigation_path: /tablette-a8/gestion
  style: |
    .sidebar-inner {
        padding: 0px !important;
    }

    .sidebarMenu li {
        padding: 20px 27px !important;
    }
    .sidebarMenu {
        border-radius: 0px;
        border-width: 0px !important;
    }

    .sidebarMenu li.active ha-icon {
    color: #ff9800 !important;
    }

    .sidebarMenu li.active::before {
        top: 0px !important;
        left: 5px !important;
        width: 150% !important;
        height: 100% !important;
        background-color: rgba(0, 0, 0, 0.6) !important;
        opacity: 0.3 !important;
        border-radius: 50px !important;
    }

    .sidebarMenu li ha-icon {
        float: right;
        color: var(--sidebar-icon-color, #000);
        margin-top: -13px;
        
    }

    h1.digitalClock {
        font-size: 28px !important;
        line-height: 5px !important;
        cursor: default !important;
        color: #ff9800 !important;
        padding-bottom: 0px !important;
        padding-top: 15px !important;
        font-weight: bold !important;
        text-align: center !important;
    }

    h2 {
        margin: 0px !important;
        font-size: 13px !important;
        line-height: 26px !important;
        font-weight: 300 !important;
        color: #ff9800 !important;
        cursor: default !important;
        padding-bottom: 0px !important;
        padding-top: 0px !important;
        text-align: center !important;

    }
  bottomCard:
    type: custom:stack-in-card
    cardOptions:
      keep:
        box_shadow: true
        margin: false
        border_radius: false
        background: false
        outer_padding: false
      cards:
        - type: horizontal-stack
          card_mod:
            style: |
              ha-card {
                border-radius: 0px;
                border-width: 0px !important;
                background: rgba(0, 0, 0, 0) !important;
              }
          cards:
            - type: custom:mushroom-chips-card
              chips:
                - type: template
                  icon: |
                    {% if [
                      states('update.home_assistant_core_update'),
                      states('update.home_assistant_operating_system_update'),
                      states('update.mosquitto_broker_update'),
                      states('update.z_wave_js_update'),
                      states('update.influxdb_update'),
                      states('update.grafana_update'),
                      states('update.studio_code_server_update'),
                      states('update.advanced_ssh_web_terminal_update'),
                      states('update.file_editor_update'),
                      states('update.samba_share_update'),
                      states('update.home_assistant_supervisor_update')
                    ] | select('eq', 'on') | list | length > 0 %}
                      mdi:update
                    {% else %}
                      mdi:check-circle-outline
                    {% endif %}
                  icon_color: |
                    {% if [
                      states('update.home_assistant_core_update'),
                      states('update.home_assistant_operating_system_update'),
                      states('update.mosquitto_broker_update'),
                      states('update.z_wave_js_update'),
                      states('update.influxdb_update'),
                      states('update.grafana_update'),
                      states('update.studio_code_server_update'),
                      states('update.advanced_ssh_web_terminal_update'),
                      states('update.file_editor_update'),
                      states('update.samba_share_update'),
                      states('update.home_assistant_supervisor_update')
                    ] | select('eq', 'on') | list | length > 0 %}
                      red
                    {% else %}
                      accent
                    {% endif %}
                  content: |
                    {% set updates = [
                      states('update.home_assistant_core_update'),
                      states('update.home_assistant_operating_system_update'),
                      states('update.mosquitto_broker_update'),
                      states('update.z_wave_js_update'),
                      states('update.influxdb_update'),
                      states('update.grafana_update'),
                      states('update.studio_code_server_update'),
                      states('update.advanced_ssh_web_terminal_update'),
                      states('update.file_editor_update'),
                      states('update.samba_share_update'),
                      states('update.home_assistant_supervisor_update')
                    ] | select('eq', 'on') | list | length %}
                    {% if updates > 0 %}
                      {{ updates }}
                    {% endif %}
                  layout: horizontal
                  tap_action:
                    action: navigate
                    navigation_path: /tablette-a8/maj
                  card_mod:
                    style: |
                      ha-card {
                        border-radius: 0px;
                        border-width: 0px !important;
                        background: rgba(0, 0, 0, 0) !important;
                        margin-left: 2.5px;
                      }
            - type: custom:mushroom-chips-card
              chips:
                - type: template
                  icon: >
                    {% set low_batteries = [
                      states('sensor.batterie_oeil_chambreparent')|int,
                      states('sensor.tablette_a8_battery_level')|int,
                      states('sensor.batterie_oeil_sejour')|int,
                      states('sensor.smoke_detector_battery_level')|int,
                      states('sensor.fibaro_door_window_sensor_2_test_battery_level')|int
                    ] %}

                    {% if low_batteries | select('lt', 10) | list | length > 0
                    %}
                      mdi:battery-alert
                    {% else %}
                      mdi:battery-charging
                    {% endif %}
                  icon_color: >
                    {% if (states('sensor.batterie_oeil_chambreparent')|int <
                    10) 
                       or (states('sensor.tablette_a8_battery_level')|int < 10)
                       or (states('sensor.batterie_oeil_sejour')|int < 10)
                       or (states('sensor.smoke_detector_battery_level')|int < 10)
                       or (states('sensor.fibaro_door_window_sensor_2_test_battery_level')|int < 10) %}
                      red
                    {% else %}
                      green
                    {% endif %}
                  content: >
                    {% set low_batteries = [
                      states('sensor.batterie_oeil_chambreparent')|int,
                      states('sensor.tablette_a8_battery_level')|int,
                      states('sensor.batterie_oeil_sejour')|int,
                      states('sensor.smoke_detector_battery_level')|int,
                      states('sensor.fibaro_door_window_sensor_2_test_battery_level')|int
                    ] %}

                    {% set count = low_batteries | select('lt', 10) | list |
                    length %}

                    {% if count > 0 %}
                      {{ count }}
                    {% endif %}
                  tap_action:
                    action: navigate
                    navigation_path: /tablette-a8/batterie
                  card_mod:
                    style: |
                      ha-card {
                        border-radius: 0px;
                        border-width: 0px !important;
                        background: rgba(0, 0, 0, 0) !important;
                        margin-left: -10px;
                      }
        - type: horizontal-stack
          card_mod:
            style: |
              ha-card {
                border-radius: 0px;
                border-width: 0px !important;
                background: rgba(0, 0, 0, 0) !important;
              }
          cards:
            - type: custom:mushroom-chips-card
              chips:
                - type: template
                  entity: >-
                    binary_sensor.fibaro_door_window_sensor_2_test_window_door_is_open
                  icon: >
                    {% if
                    is_state('binary_sensor.fibaro_door_window_sensor_2_test_window_door_is_open',
                    'on') %}
                      mdi:door-open
                    {% else %}
                      mdi:door-closed
                    {% endif %}
                  icon_color: >
                    {% if
                    is_state('binary_sensor.fibaro_door_window_sensor_2_test_window_door_is_open',
                    'on') %}
                      red
                    {% else %}
                      green
                    {% endif %}
                  tap_action:
                    action: more-info
                  layout: horizontal
                  card_mod:
                    style: |
                      ha-card {
                        border-radius: 0px;
                        border-width: 0px !important;
                        background: rgba(0, 0, 0, 0) !important;
                        margin-left: 2.5px;
                      }
            - type: custom:mushroom-chips-card
              chips:
                - type: template
                  entity: alarm_control_panel.alarmo
                  icon: |
                    {% if is_state('alarm_control_panel.alarmo', 'disarmed') %}
                      mdi:shield-off
                    {% else %}
                      mdi:shield-lock
                    {% endif %}
                  icon_color: |
                    {% if is_state('alarm_control_panel.alarmo', 'disarmed') %}
                      red
                    {% else %}
                      green
                    {% endif %}
                  tap_action:
                    action: navigate
                    navigation_path: /tablette-a8/alarme
                  card_mod:
                    style: |
                      ha-card {
                        border-radius: 0px;
                        border-width: 0px !important;
                        background: rgba(0, 0, 0, 0) !important;
                        margin-left: -10px;
                      }
        - type: picture
          image: /local/images/MR.png
          card_mod:
            style: |
              ha-card {
                border-radius: 0px !important;
                border-width: 0px !important;
              }
              img {
                width: 100% !important;
                margin-left: 0px;
              }
    cardStyle: |
      ha-card {
        border: none !important;
        border-radius: 0px !important;
        height: unset !important;
      }

```
</details>
<details>
  <summary>Entête</summary>

```yaml
type: custom:mushroom-chips-card
chips:
  - type: action
    tap_action:
      action: call-service
      service: browser_mod.popup
      data:
        title: Scan le code pour te connecter !
        content:
          type: picture
          image: local/images/Wifiqr.png
          tap_action:
            action: none
          hold_action:
            action: none
        entity: input_button.qr
    icon_color: accent
    icon: mdi:wifi-plus
    card_mod:
      style: |
        ha-card {
          border-width: 0px !important;
          background: rgba(0, 0, 0, 0) !important;
        }
  - type: template
    entity: person.x
    content: Raphaël
    icon: |
      {% if is_state('person.x', 'home') %}
        mdi:account
      {% else %}
        mdi:account-off
      {% endif %}
    icon_color: |
      {% if is_state('person.x', 'home') %}
        green
      {% else %}
        red
      {% endif %}
    tap_action:
      action: more-info
    card_mod:
      style: |
        ha-card {
          border-width: 0px !important;
          background: rgba(0, 0, 0, 0) !important;
        }
  - type: template
    entity: person.x
    content: x
    icon: |
      {% if is_state('person.x', 'home') %}
        mdi:account
      {% else %}
        mdi:account-off
      {% endif %}
    icon_color: |
      {% if is_state('person.x', 'home') %}
        green
      {% else %}
        red
      {% endif %}
    tap_action:
      action: more-info
    card_mod:
      style: |
        ha-card {
          border-width: 0px !important;
          background: rgba(0, 0, 0, 0) !important;
        }
  - type: template
    entity: alarm_control_panel.alarmo
    icon: |
      {% if is_state('alarm_control_panel.alarmo', 'disarmed') %}
        mdi:shield-off
      {% else %}
        mdi:shield-lock
      {% endif %}
    icon_color: |
      {% if is_state('alarm_control_panel.alarmo', 'disarmed') %}
        red
      {% else %}
        green
      {% endif %}
    content: |
      {% if is_state('alarm_control_panel.alarmo', 'disarmed') %}
        Alarme désactivée
      {% else %}
        Alarme activée
      {% endif %}
    tap_action:
      action: navigate
      navigation_path: /tablette-a8/alarme
    card_mod:
      style: |
        ha-card {
          border-width: 0px !important;
          background: rgb(0, 0, 0, 0) !important;
        }
layout_options:
  grid_columns: 4
  grid_rows: auto
alignment: start


```
</details>
<details>
  <summary>Carte température</summary>

```yaml
type: custom:stack-in-card
mode: vertical
keep:
  box_shadow: true
  margin: true
  border_radius: true
  background: true
  outer_padding: false
card_mod:
  style: |
    ha-card {
      border-width: 0px !important;
      background: rgba(0, 0, 0, 0); #0.3=30%
      box-shadow: none;
    }
cards:
  - type: horizontal-stack
    cards:
      - type: custom:flex-horseshoe-card
        entities:
          - entity: sensor.temperature_chambre1
            attribute: temperature
            decimals: 1
            unit: °C
            area: Chambre 1
        show:
          horseshoe_style: lineargradient
        layout:
          states:
            - id: 0
              entity_index: 0
              xpos: 50
              ypos: 60
              styles:
                - font-size: 3.5em;
          areas:
            - id: 0
              entity_index: 0
              xpos: 50
              ypos: 35
              styles:
                - font-size: 1.5em;
                - opacity: 0.8;
        horseshoe_scale:
          min: 0
          max: 40
        color_stops:
          "16": "#FFF6E3"
          "17": "#FFE9B9"
          "18": "#FFDA8A"
          "19": "#FFCB5B"
          "20": "#FFBF37"
          "21": "#ffb414"
          "22": "#FFAD12"
          "23": "#FFA40E"
          "24": "#FF9C0B"
          "25": "#FF8C06"
        card_mod:
          style: |
            ha-card {
              border-width: 0px !important;
              background: rgba(0, 0, 0, 0); #0.3=30%
              box-shadow: none;
            }
      - type: custom:flex-horseshoe-card
        entities:
          - entity: sensor.temperature_chambre2
            attribute: temperature
            decimals: 1
            unit: °C
            area: Chambre 2
        show:
          horseshoe_style: lineargradient
        layout:
          states:
            - id: 0
              entity_index: 0
              xpos: 50
              ypos: 60
              styles:
                - font-size: 3.5em;
          areas:
            - id: 0
              entity_index: 0
              xpos: 50
              ypos: 35
              styles:
                - font-size: 1.5em;
                - opacity: 0.8;
        horseshoe_scale:
          min: 0
          max: 40
        color_stops:
          "16": "#FFF6E3"
          "17": "#FFE9B9"
          "18": "#FFDA8A"
          "19": "#FFCB5B"
          "20": "#FFBF37"
          "21": "#ffb414"
          "22": "#FFAD12"
          "23": "#FFA40E"
          "24": "#FF9C0B"
          "25": "#FF8C06"
        card_mod:
          style: |
            ha-card {
              border-width: 0px !important;
              background: rgba(0, 0, 0, 0); #0.3=30%
              box-shadow: none;
            }
      - type: custom:flex-horseshoe-card
        entities:
          - entity: sensor.temperature_chambreparent
            attribute: temperature
            decimals: 1
            unit: °C
            area: Parent
        show:
          horseshoe_style: lineargradient
        layout:
          states:
            - id: 0
              entity_index: 0
              xpos: 50
              ypos: 60
              styles:
                - font-size: 3.5em;
          areas:
            - id: 0
              entity_index: 0
              xpos: 50
              ypos: 35
              styles:
                - font-size: 1.5em;
                - opacity: 0.8;
        horseshoe_scale:
          min: 0
          max: 40
        color_stops:
          "16": "#FFF6E3"
          "17": "#FFE9B9"
          "18": "#FFDA8A"
          "19": "#FFCB5B"
          "20": "#FFBF37"
          "21": "#ffb414"
          "22": "#FFAD12"
          "23": "#FFA40E"
          "24": "#FF9C0B"
          "25": "#FF8C06"
        card_mod:
          style: |
            ha-card {
              border-width: 0px !important;
              background: rgba(0, 0, 0, 0); #0.3=30%
              box-shadow: none;
            }
  - type: horizontal-stack
    cards:
      - type: custom:flex-horseshoe-card
        entities:
          - entity: sensor.temperature_bureau
            attribute: temperature
            decimals: 1
            unit: °C
            area: Bureau
        show:
          horseshoe_style: lineargradient
        layout:
          states:
            - id: 0
              entity_index: 0
              xpos: 50
              ypos: 60
              styles:
                - font-size: 3.5em;
          areas:
            - id: 0
              entity_index: 0
              xpos: 50
              ypos: 35
              styles:
                - font-size: 1.5em;
                - opacity: 0.8;
        horseshoe_scale:
          min: 0
          max: 40
        color_stops:
          "16": "#FFF6E3"
          "17": "#FFE9B9"
          "18": "#FFDA8A"
          "19": "#FFCB5B"
          "20": "#FFBF37"
          "21": "#ffb414"
          "22": "#FFAD12"
          "23": "#FFA40E"
          "24": "#FF9C0B"
          "25": "#FF8C06"
        card_mod:
          style: |
            ha-card {
              border-width: 0px !important;
              background: rgba(0, 0, 0, 0); #0.3=30%
              box-shadow: none;
            }
      - type: custom:flex-horseshoe-card
        entities:
          - entity: sensor.temperature_sdb
            attribute: temperature
            decimals: 1
            unit: °C
            area: Salle de bain
        show:
          horseshoe_style: lineargradient
        layout:
          states:
            - id: 0
              entity_index: 0
              xpos: 50
              ypos: 60
              styles:
                - font-size: 3.5em;
          areas:
            - id: 0
              entity_index: 0
              xpos: 50
              ypos: 35
              styles:
                - font-size: 1.5em;
                - opacity: 0.8;
        horseshoe_scale:
          min: 0
          max: 40
        color_stops:
          "16": "#FFF6E3"
          "17": "#FFE9B9"
          "18": "#FFDA8A"
          "19": "#FFCB5B"
          "20": "#FFBF37"
          "21": "#ffb414"
          "22": "#FFAD12"
          "23": "#FFA40E"
          "24": "#FF9C0B"
          "25": "#FF8C06"
        card_mod:
          style: |
            ha-card {
              border-width: 0px !important;
              background: rgba(0, 0, 0, 0); #0.3=30%
              box-shadow: none;
            }
      - type: custom:flex-horseshoe-card
        entities:
          - entity: sensor.temperature_sejour
            attribute: temperature
            decimals: 1
            unit: °C
            area: Séjour
        show:
          horseshoe_style: lineargradient
        layout:
          states:
            - id: 0
              entity_index: 0
              xpos: 50
              ypos: 60
              styles:
                - font-size: 3.5em;
          areas:
            - id: 0
              entity_index: 0
              xpos: 50
              ypos: 35
              styles:
                - font-size: 1.5em;
                - opacity: 0.8;
        horseshoe_scale:
          min: 0
          max: 40
        color_stops:
          "16": "#FFF6E3"
          "17": "#FFE9B9"
          "18": "#FFDA8A"
          "19": "#FFCB5B"
          "20": "#FFBF37"
          "21": "#ffb414"
          "22": "#FFAD12"
          "23": "#FFA40E"
          "24": "#FF9C0B"
          "25": "#FF8C06"
        card_mod:
          style: |
            ha-card {
              border-width: 0px !important;
              background: rgba(0, 0, 0, 0); #0.3=30%
              box-shadow: none;
            }


```
</details>
<details>
  <summary>Carte météo</summary>

```yaml
type: custom:stack-in-card
mode: horizontal
keep:
  box_shadow: true
  margin: true
  border_radius: true
  background: true
  outer_padding: false
card_mod:
  style: |
    ha-card {
      border-width: 0px !important;
      background: rgba(0, 0, 0, 0); #0.3=30%
      box-shadow: none;
    }
cards:
  - type: custom:mini-graph-card
    entities:
      - entity: sensor.x
        aggregate_func: max
        name: Max
        color: "#e74c3c"
      - entity: sensor.x
        aggregate_func: min
        name: Min
      - entity: sensor.x
        aggregate_func: Moyenne
        name: Moyenne
        color: "#ff9800"
    name: Température ext. sur une semaine
    hours_to_show: 168
    group_by: date
    icon: mdi:home-thermometer-outline
    card_mod:
      style: |
        ha-card {
          border-radius: 0px;
          border-width: 0px !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
        }
        .icon {
            color: #ff9800 !important;
        }
  - type: weather-forecast
    entity: weather.X
    show_current: true
    show_forecast: true
    forecast_type: daily
    name: X
    secondary_info_attribute: wind_speed
    view_layout:
      position: main
    card_mod:
      style: |
        ha-card {
          border-width: 0px !important;
          card-border-width: 0px;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
layout_options:
  grid_columns: 7
  grid_rows: auto


```
</details>

## Chauffage
![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/02.jpg)
<details>
  <summary>Carte de gauche</summary>

```yaml
type: custom:stack-in-card
keep:
  margin: true
  box_shadow: true
  background: true
cards:
  - type: custom:mushroom-climate-card
    entity: climate.chambre_parent
    tap_action:
      action: false
    name: Chambre parent
    icon: mdi:thermometer
    primary_info: name
    secondary_info: state
    show_temperature_control: true
    hvac_modes:
      - "off"
      - heat
      - cool
    collapsible_controls: false
    fill_container: false
    layout: horizontal
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
  - type: custom:mushroom-entity-card
    entity: switch.electrovanne_chambreparent
    icon: mdi:valve
    layout: horizontal
    primary_info: name
    name: Statut électrovanne
    secondary_info: none
    tap_action:
      action: false
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
          margin-top: -15px;
          margin-bottom: -50px;
          margin-left: 10px;
        }
        :host {
          --spacing: 0px !important;
        }
  - type: custom:mini-graph-card
    entities:
      - entity: sensor.temperature_chambreparent
        name: Température dernière 48h
        color: "#ff9800"
    hours_to_show: 48
    points_per_hour: 1
    line_width: 2
    font_size: 50
    animate: true
    show:
      name: true
      icon: false
      state: true
      legend: false
      fill: fade
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
  - type: custom:mushroom-climate-card
    entity: climate.chambre_1
    tap_action:
      action: false
    name: Chambre 1
    icon: mdi:thermometer
    primary_info: name
    secondary_info: state
    show_temperature_control: true
    hvac_modes:
      - "off"
      - heat
      - cool
    collapsible_controls: false
    fill_container: false
    layout: horizontal
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
  - type: custom:mushroom-entity-card
    entity: switch.electrovanne_chambre1
    icon: mdi:valve
    layout: horizontal
    primary_info: name
    name: Statut électrovanne
    secondary_info: none
    tap_action:
      action: false
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
          margin-top: -15px;
          margin-bottom: -50px;
          margin-left: 10px;
        }
        :host {
          --spacing: 0px !important;
        }
  - type: custom:mini-graph-card
    entities:
      - entity: sensor.temperature_chambre1
        name: Température dernière 48h
        color: "#ff9800"
    hours_to_show: 48
    points_per_hour: 1
    line_width: 2
    font_size: 50
    animate: true
    show:
      name: true
      icon: false
      state: true
      legend: false
      fill: fade
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
  - type: custom:mushroom-climate-card
    entity: climate.chambre_2
    tap_action:
      action: false
    name: Chambre 2
    icon: mdi:thermometer
    primary_info: name
    secondary_info: state
    show_temperature_control: true
    hvac_modes:
      - "off"
      - heat
      - cool
    collapsible_controls: false
    fill_container: false
    layout: horizontal
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
  - type: custom:mushroom-entity-card
    entity: switch.electrovanne_chambre2
    icon: mdi:valve
    layout: horizontal
    primary_info: name
    name: Statut électrovanne
    secondary_info: none
    tap_action:
      action: false
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
          margin-top: -15px;
          margin-bottom: -50px;
          margin-left: 10px;
        }
        :host {
          --spacing: 0px !important;
        }
  - type: custom:mini-graph-card
    entities:
      - entity: sensor.temperature_chambre2
        name: Température dernière 48h
        color: "#ff9800"
    hours_to_show: 48
    points_per_hour: 1
    line_width: 2
    font_size: 50
    animate: true
    show:
      name: true
      icon: false
      state: true
      legend: false
      fill: fade
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
card_mod:
  style: |
    ha-card {
      border-radius: 30px;
      border-width: 0px !important;
      background: rgba(0, 0, 0, 0); #0.3=30%
      box-shadow: none;
    }


```
</details>
<details>
  <summary>Carte de droite</summary>

```yaml
type: custom:stack-in-card
keep:
  margin: true
  box_shadow: true
  background: true
cards:
  - type: custom:mushroom-climate-card
    entity: climate.sejour
    tap_action:
      action: false
    name: Séjour
    icon: mdi:thermometer
    primary_info: name
    secondary_info: state
    show_temperature_control: true
    hvac_modes:
      - "off"
      - heat
      - cool
    collapsible_controls: false
    fill_container: false
    layout: horizontal
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
  - type: custom:mushroom-entity-card
    entity: switch.electrovanne_sejour
    icon: mdi:valve
    layout: horizontal
    primary_info: name
    name: Statut électrovanne
    secondary_info: none
    tap_action:
      action: false
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
          margin-top: -15px;
          margin-bottom: -50px;
          margin-left: 10px;
        }
        :host {
          --spacing: 0px !important;
        }
  - type: custom:mini-graph-card
    entities:
      - entity: sensor.temperature_sejour
        name: Température dernière 48h
        color: "#ff9800"
    hours_to_show: 48
    points_per_hour: 1
    line_width: 2
    font_size: 50
    animate: true
    show:
      name: true
      icon: false
      state: true
      legend: false
      fill: fade
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
  - type: custom:mushroom-climate-card
    entity: climate.salle_de_bain
    tap_action:
      action: false
    name: Salle de bain
    icon: mdi:thermometer
    primary_info: name
    secondary_info: state
    show_temperature_control: true
    hvac_modes:
      - "off"
      - heat
      - cool
    collapsible_controls: false
    fill_container: false
    layout: horizontal
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
  - type: custom:mushroom-entity-card
    entity: switch.electrovanne_sdb
    icon: mdi:valve
    layout: horizontal
    primary_info: name
    name: Statut électrovanne
    secondary_info: none
    tap_action:
      action: false
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
          margin-top: -15px;
          margin-bottom: -50px;
          margin-left: 10px;
        }
        :host {
          --spacing: 0px !important;
        }
  - type: custom:mini-graph-card
    entities:
      - entity: sensor.temperature_sdb
        name: Température dernière 48h
        color: "#ff9800"
    hours_to_show: 48
    points_per_hour: 1
    line_width: 2
    font_size: 50
    animate: true
    show:
      name: true
      icon: false
      state: true
      legend: false
      fill: fade
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
  - type: custom:mushroom-climate-card
    entity: climate.bureau
    tap_action:
      action: false
    name: Bureau
    icon: mdi:thermometer
    primary_info: name
    secondary_info: state
    show_temperature_control: true
    hvac_modes:
      - "off"
      - heat
      - cool
    collapsible_controls: false
    fill_container: false
    layout: horizontal
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
  - type: custom:mushroom-entity-card
    entity: switch.electrovanne_bureau
    icon: mdi:valve
    layout: horizontal
    primary_info: name
    name: Statut électrovanne
    secondary_info: none
    tap_action:
      action: false
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
          margin-top: -15px;
          margin-bottom: -50px;
          margin-left: 10px;
        }
        :host {
          --spacing: 0px !important;
        }
  - type: custom:mini-graph-card
    entities:
      - entity: sensor.temperature_bureau
        name: Température dernière 48h
        color: "#ff9800"
    hours_to_show: 48
    points_per_hour: 1
    line_width: 2
    font_size: 50
    animate: true
    show:
      name: true
      icon: false
      state: true
      legend: false
      fill: fade
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
card_mod:
  style: |
    ha-card {
      border-radius: 30px;
      border-width: 0px !important;
      background: rgba(0, 0, 0, 0); #0.3=30%
      box-shadow: none;
    }


```
</details>

## Musique
![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/03.jpg)

<details>
  <summary>Carte sonos</summary>

```yaml
type: custom:mini-media-player
entity: media_player.sejour
artwork: full-cover
toggle_power: false
card_mod:
  style: |
    ha-card {
      border-width: 0px !important;
      background: rgba(0, 0, 0, 0);
      box-shadow: none;
    }


```
</details>

## Agenda
![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/04.jpg)
<details>
  <summary>Agenda haut</summary>

```yaml
type: custom:atomic-calendar-revive
enableModeChange: true
entities:
  - entity: calendar.x
    name: x@gmail.com
  - entity: calendar.x
    name: x@gmail.com
defaultMode: Calendar
disableCalLink: true
calShowDescription: false
disableCalEventLink: false
dimFinishedEvents: true
showDeclined: false
hideFinishedEvents: false
showDate: true
dateFormat: dddd D MMMM
compactMode: false
offsetHeaderDate: false
allDayBottom: true
showNoEventsForToday: false
showHiddenText: true
showWeekNumber: false
showLastCalendarWeek: true
card_mod:
  style: |
    ha-card {
      border-width: 0px !important;
      card-border-width: 0px;
      background: rgba(0, 0, 0, 0); #0.3=30%
      box-shadow: none;
    {


```
</details>

<details>
  <summary>Agenda bas</summary>

```yaml
type: custom:atomic-calendar-revive
enableModeChange: true
entities:
  - entity: calendar.x
    name: x94@gmail.com
  - entity: calendar.x
    name: x@gmail.com
compactMode: true
card_mod:
  style: |
    ha-card {
      border-width: 0px !important;
      card-border-width: 0px;
      background: rgba(0, 0, 0, 0); #0.3=30%
      box-shadow: none;
    {


```
</details>

## Todo-list
![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/05.jpg)
<details>
  <summary>Todo-list</summary>

```yaml
type: todo-list
entity: todo.liste_dachats
title: Liste d'achats
card_mod:
  style: |
    ha-card {
      border-radius: 30px;
      border-width: 0px !important;
      background: rgba(0, 0, 0, 0); #0.3=30%
      box-shadow: none;
    }


```
</details>

## Paramètre
![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/06.jpg)
<details>
  <summary>Menu paramètre</summary>
  
```yaml
type: custom:stack-in-card
mode: vertical
keep:
  box_shadow: true
  margin: true
  border_radius: true
  background: true
  outer_padding: false
card_mod:
  style: |
    ha-card {
      border-width: 0px !important;
      background: rgba(0, 0, 0, 0); #0.3=30%
      box-shadow: none;
    }
cards:
  - type: custom:button-card
    icon: phu:raspberry-pi
    tap_action:
      action: navigate
      navigation_path: /tablette-a8/rpi
    styles:
      card:
        - width: 100px
        - height: 100px
        - background-color: rgba(50, 251, 253, 0.7)
        - clip-path: polygon(25% 6%, 75% 6%, 100% 50%, 75% 94%, 25% 94%, 0% 50%)
        - border: 2px solid rgba(0, 0, 0, 0.1)
        - box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.2)
      icon:
        - color: white
        - font-size: 30px
        - padding: 10px
      custom_fields:
        outline:
          - position: absolute
          - top: 0.5px
          - left: 0.5px
          - width: calc(99%)
          - height: calc(99%)
          - clip-path: polygon(25% 6%, 75% 6%, 100% 50%, 75% 94%, 25% 94%, 0% 50%)
          - background: "#002A4D"
          - z-index: -1
    custom_fields:
      outline: ""
    card_mod:
      style: |
        ha-card {
          margin-left: 159px
        }
  - type: custom:button-card
    icon: mdi:update
    tap_action:
      action: navigate
      navigation_path: /tablette-a8/maj
    styles:
      card:
        - width: 100px
        - height: 100px
        - background-color: rgba(50, 251, 253, 0.7)
        - clip-path: polygon(25% 6%, 75% 6%, 100% 50%, 75% 94%, 25% 94%, 0% 50%)
        - border: 2px solid rgba(0, 0, 0, 0.1)
        - box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.2)
      icon:
        - color: white
        - font-size: 30px
        - padding: 10px
      custom_fields:
        outline:
          - position: absolute
          - top: 0.5px
          - left: 0.5px
          - width: calc(99%)
          - height: calc(99%)
          - clip-path: polygon(25% 6%, 75% 6%, 100% 50%, 75% 94%, 25% 94%, 0% 50%)
          - background: "#002A4D"
          - z-index: -1
    custom_fields:
      outline: ""
    card_mod:
      style: |
        ha-card {
          margin-left: 80px ;
          margin-top: -61px;
        }
  - type: custom:button-card
    icon: mdi:battery-charging
    tap_action:
      action: navigate
      navigation_path: /tablette-a8/batterie
    styles:
      card:
        - width: 100px
        - height: 100px
        - background-color: rgba(50, 251, 253, 0.7)
        - clip-path: polygon(25% 6%, 75% 6%, 100% 50%, 75% 94%, 25% 94%, 0% 50%)
        - border: 2px solid rgba(0, 0, 0, 0.1)
        - box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.2)
      icon:
        - color: white
        - font-size: 30px
        - padding: 10px
      custom_fields:
        outline:
          - position: absolute
          - top: 0.5px
          - left: 0.5px
          - width: calc(99%)
          - height: calc(99%)
          - clip-path: polygon(25% 6%, 75% 6%, 100% 50%, 75% 94%, 25% 94%, 0% 50%)
          - background: "#002A4D"
          - z-index: -1
    custom_fields:
      outline: ""
    card_mod:
      style: |
        ha-card {
          margin-left: 159px ;
          margin-top: -62px;
        }
  - type: custom:button-card
    icon: mdi:lightning-bolt
    tap_action:
      action: navigate
      navigation_path: /tablette-a8/energie
    styles:
      card:
        - width: 100px
        - height: 100px
        - background-color: rgba(50, 251, 253, 0.7)
        - clip-path: polygon(25% 6%, 75% 6%, 100% 50%, 75% 94%, 25% 94%, 0% 50%)
        - border: 2px solid rgba(0, 0, 0, 0.1)
        - box-shadow: 2px 2px 8px rgba(0, 0, 0, 0.2)
      icon:
        - color: white
        - font-size: 30px
        - padding: 10px
      custom_fields:
        outline:
          - position: absolute
          - top: 0.5px
          - left: 0.5px
          - width: calc(99%)
          - height: calc(99%)
          - clip-path: polygon(25% 6%, 75% 6%, 100% 50%, 75% 94%, 25% 94%, 0% 50%)
          - background: "#002A4D"
          - z-index: -1
    custom_fields:
      outline: ""
    card_mod:
      style: |
        ha-card {
          margin-left: 80px ;
          margin-top: -61px;
        }
  - type: custom:button-card
    icon: mdi:water
    tap_action:
      action: navigate
      navigation_path: /tablette-a8/eau
    styles:
      card:
        - width: 100px
        - height: 100px
        - background-color: rgba(50, 251, 253, 0.7)
        - clip-path: polygon(25% 6%, 75% 6%, 100% 50%, 75% 94%, 25% 94%, 0% 50%)
        - border: 2px solid rgba(0, 0, 0, 0.1)
        - box-shadow: 2px 2px 8px rba(0gba(0, 0, 0, 0.2)
      icon:
        - color: white
        - font-size: 30px
        - padding: 10px
      custom_fields:
        outline:
          - position: absolute
          - top: 0.5px
          - left: 0.5px
          - width: calc(99%)
          - height: calc(99%)
          - clip-path: polygon(25% 6%, 75% 6%, 100% 50%, 75% 94%, 25% 94%, 0% 50%)
          - background: "#002A4D"
          - z-index: -1
    custom_fields:
      outline: ""
    card_mod:
      style: |
        ha-card {
          margin-left: 0px ;
          margin-top: -62px;
        }


```
</details>

## RPi
  ![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/07.jpg)
<details>
  <summary>Carte Raspberry Pi</summary>

```yaml
type: custom:stack-in-card
mode: vertical
keep:
  box_shadow: true
  margin: true
  border_radius: true
  background: true
  outer_padding: false
cards:
  - type: vertical-stack
    cards:
      - type: picture
        image: /local/images/RPI1.png
        card_mod:
          style: |
            ha-card {
              border-radius: 0px;
              background: rgba(0, 0, 0, 0); #0.3=30%
            }
  - type: vertical-stack
    cards:
      - type: horizontal-stack
        cards:
          - type: custom:mushroom-entity-card
            entity: sensor.home_assistant_host_os_agent_version
            icon_type: none
            name: Version OS
            layout: vertical
            card_mod:
              style: |
                ha-card {
                  border-width: 0px !important;
                  background: rgba(0, 0, 0, 0); #0.3=30%
                }
          - type: custom:mushroom-entity-card
            entity: sensor.uptime
            icon_type: none
            name: Uptime
            layout: vertical
            card_mod:
              style: |
                ha-card {
                  border-width: 0px !important;
                  background: rgba(0, 0, 0, 0); #0.3=30%
                }
          - type: custom:mushroom-entity-card
            entity: sensor.system_monitor_adresse_ipv4_end0
            icon_type: none
            name: IP
            layout: vertical
            card_mod:
              style: |
                ha-card {
                  border-width: 0px !important;
                  background: rgba(0, 0, 0, 0); #0.3=30%
                }
      - type: custom:mini-graph-card
        entities:
          - sensor.system_monitor_utilisation_du_disque
        color_thresholds:
          - value: 49
            color: grey
          - value: 50
            color: "#ff9800"
          - value: 80
            color: "#ff0000"
        height: 30
        line_width: 2
        font_size: 70
        hours_to_show: 24
        points_per_hour: 1
        show:
          extrema: false
          fill: true
          average: false
          name: false
          icon: false
          state: false
          graph: line
        card_mod:
          style: |
            ha-card { 
              border-radius: 0px;
              border-width: 0px !important;
              #font-size: 20px !important;
              margin-top: -20px;
              background: rgba(0, 0, 0, 0); #0.3=30%
            }
      - type: custom:bar-card
        entities:
          - entity: sensor.system_monitor_utilisation_du_disque
        name: SSD 128GB NVMe M.2 PCIe Gen3x4
        entity_row: true
        icon: phu:seagate-ssd-m2
        align: split
        height: 30
        columns: 1
        max: 100
        positions:
          icon: inside
          indicator: inside
          name: inside
          value: inside
        unit_of_measurement: "%"
        severity:
          - color: grey
            from: 0
            to: 50
          - color: "#ff9800"
            from: 50
            to: 80
          - color: "#ff0000"
            from: 80
            to: 100
        card_mod:
          style: |
            ha-card { 
                --paper-item-icon-color: 'var(--text-primary-color';
                border-width: 0px !important;
                margin-top: -10px;
                background: rgba(0, 0, 0, 0); #0.3=30%
            }
      - type: custom:mini-graph-card
        entities:
          - sensor.system_monitor_utilisation_de_la_memoire
        name: null
        color_thresholds:
          - value: 49
            color: grey
          - value: 50
            color: "#ff9800"
          - value: 80
            color: "#ff0000"
        height: 30
        line_width: 2
        font_size: 70
        hours_to_show: 24
        points_per_hour: 1
        show:
          extrema: false
          fill: true
          average: false
          name: false
          icon: false
          state: false
          graph: line
        card_mod:
          style: |
            ha-card { 
              border-radius: 0px;
              border-width: 0px !important;
              #font-size: 20px !important;
              margin-top: -10px;
              background: rgba(0, 0, 0, 0); #0.3=30%
            }
      - type: custom:bar-card
        entities:
          - entity: sensor.system_monitor_utilisation_de_la_memoire
        name: RAM 8GB
        entity_row: true
        icon: phu:ram-memory
        height: 30
        align: split
        columns: 1
        max: 100
        positions:
          icon: inside
          indicator: inside
          name: inside
          value: inside
        unit_of_measurement: "%"
        severity:
          - color: grey
            from: 0
            to: 50
          - color: "#ff9800"
            from: 50
            to: 80
          - color: "#ff0000"
            from: 80
            to: 100
        card_mod:
          style: |
            ha-card { 
                --paper-item-icon-color: 'var(--text-primary-color';
                border-width: 0px !important;
                margin-top: -10px;
                background: rgba(0, 0, 0, 0); #0.3=30%
            }
      - type: custom:mini-graph-card
        entities:
          - sensor.system_monitor_utilisation_du_processeur
        name: null
        color_thresholds:
          - value: 49
            color: grey
          - value: 50
            color: "#ff9800"
          - value: 80
            color: "#ff0000"
        height: 30
        line_width: 2
        font_size: 70
        hours_to_show: 24
        points_per_hour: 1
        show:
          extrema: false
          fill: true
          average: false
          name: false
          icon: false
          state: false
          graph: line
        card_mod:
          style: |
            ha-card { 
              border-radius: 0px;
              border-width: 0px !important;
              #font-size: 20px !important;
              margin-top: -10px;
              background: rgba(0, 0, 0, 0); #0.3=30%
            }
      - type: custom:bar-card
        entities:
          - entity: sensor.system_monitor_utilisation_du_processeur
        name: ARM Cortex-A76 Quad-Core 2.4 GHz
        entity_row: true
        color: "#ff9800"
        show_icon: true
        height: 30
        align: split
        columns: 1
        max: 100
        positions:
          icon: inside
          indicator: inside
          name: inside
          value: inside
        unit_of_measurement: "%"
        severity:
          - color: grey
            from: 0
            to: 50
          - color: "#ff9800"
            from: 50
            to: 80
          - color: "#ff0000"
            from: 80
            to: 100
        card_mod:
          style: |
            ha-card { 
                --paper-item-icon-color: 'var(--text-primary-color';
                border-width: 0px !important;
                margin-top: -10px;
                background: rgba(0, 0, 0, 0); #0.3=30%
            }
      - type: custom:mini-graph-card
        entities:
          - sensor.system_monitor_temperature_du_processeur
        name: null
        color_thresholds:
          - value: 49
            color: grey
          - value: 50
            color: "#ff9800"
          - value: 60
            color: "#ff0000"
        height: 30
        line_width: 2
        font_size: 70
        hours_to_show: 24
        points_per_hour: 1
        show:
          extrema: false
          fill: true
          average: false
          name: false
          icon: false
          state: false
          graph: line
        card_mod:
          style: |
            ha-card { 
              border-radius: 0px;
              border-width: 0px !important;
              #font-size: 20px !important;
              margin-top: -10px;
              background: rgba(0, 0, 0, 0); #0.3=30%
            }
      - type: custom:bar-card
        entities:
          - entity: sensor.system_monitor_temperature_du_processeur
        name: Temperature processeur
        height: 30
        entity_row: true
        icon: mdi:thermometer
        color: "#ff9800"
        align: split
        columns: 1
        max: 70
        positions:
          icon: inside
          indicator: inside
          name: inside
          value: inside
        unit_of_measurement: null
        severity:
          - color: grey
            from: 0
            to: 50
          - color: "#ff9800"
            from: 50
            to: 60
          - color: "#ff0000"
            from: 60
            to: 100
        card_mod:
          style: |
            ha-card { 
                --paper-item-icon-color: 'var(--text-primary-color';
                border-width: 0px !important;
                margin-top: -10px;
                background: rgba(0, 0, 0, 0); #0.3=30%
            }
      - type: custom:apexcharts-card
        series:
          - entity: sensor.system_monitor_debit_du_reseau_entrant_via_end0
            name: Entrant
            color: grey
          - entity: sensor.system_monitor_debit_du_reseau_sortant_via_end0
            name: Sortant
            color: "#ff9800"
            invert: true
        layout: minimal
        graph_span: 1h
        update_interval: 1min
        apex_config:
          chart:
            height: 150px
          legend:
            show: false
          fill:
            type: gradient
            gradient:
              type: vertical
              shadeIntensity: 0.1
              inverseColors: false
              opacityFrom: 0.5
              opacityTo: 0.1
              stops:
                - 0
        all_series_config:
          stroke_width: 2
          opacity: 0.1
          type: area
          curve: smooth
          group_by:
            func: avg
            duration: 1min
        card_mod:
          style: |
            ha-card { 
              border-radius: 0px;
              border-width: 0px !important;
              #font-size: 20px !important;
              margin-top: -10px;
              background: rgba(0, 0, 0, 0); #0.3=30%
            }
card_mod:
  style: |
    ha-card {
      border-radius: 10px;
      border-width: 0px !important;
      background: rgba(0, 0, 0, 0); #0.3=30%
    }


```
</details>

## Batterie
![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/08.jpg)
<details>
  <summary>Carte batterie</summary>

```yaml
type: custom:stack-in-card
mode: vertical
keep:
  box_shadow: true
  margin: true
  border_radius: true
  background: true
  outer_padding: false
cards:
  - type: custom:mushroom-title-card
    #title: Statut des batteries
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          border: none !important;
          margin-bottom: -15px !important;
          margin-top: -25px !important;
          margin-left: 60px !important;
        }
  - type: custom:battery-state-card
    entities:
      - sensor.batterie_oeil_chambreparent
      - sensor.tablette_a8_battery_level
      - sensor.batterie_oeil_sejour
      - sensor.smoke_detector_battery_level
      - sensor.fibaro_door_window_sensor_2_test_battery_level
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          border: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          margin-bottom: -25px !important;
        }
        .card-content div {
          margin-top: -0px !important;
          margin-bottom: 0px !important;
        }
card_mod:
  style: |
    ha-card {
      border-width: 0px !important;
      background: rgba(0, 0, 0, 0); #0.3=30%
      box-shadow: none;
    }


```
</details>

## Update
![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/09.jpg)
<details>
  <summary>Carte update</summary>

```yaml
type: custom:stack-in-card
mode: vertical
keep:
  box_shadow: true
  margin: true
  border_radius: true
  background: true
  outer_padding: false
cards:
  - type: custom:mushroom-title-card
    #title: Statut des mises à jour
    card_mod:
      style: |
        ha-card {
          box-shadow: none !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          border: none !important;
          margin-bottom: -15px !important;
          margin-top: -25px !important;
          margin-left: 40px !important;
        }
  - type: entities
    entities:
      - entity: update.home_assistant_core_update
      - entity: update.home_assistant_operating_system_update
      - entity: update.home_assistant_supervisor_update
      - entity: update.mosquitto_broker_update
      - entity: update.z_wave_js_update
      - entity: update.influxdb_update
      - entity: update.grafana_update
      - entity: update.studio_code_server_update
      - entity: update.advanced_ssh_web_terminal_update
      - entity: update.file_editor_update
      - entity: update.samba_share_update
    show_header_toggle: false
    state_color: true
    card_mod:
      style:
        .: |
          ha-card {
            box-shadow: none !important;
            border: none !important;
            background: rgba(0, 0, 0, 0); #0.3=30%
          }
          .card-content div {
            #margin-top: -20px !important;
            #margin-bottom: -20px !important;
          }
        "#states":
          hui-update-entity-row:
            $:
              hui-generic-entity-row:
                $: |
                  state-badge {
                   transform: scale(90%) !important;
                  }
card_mod:
  style: |
    ha-card {
      border-radius: 30px;
      border-width: 0px !important;
      background: rgba(0, 0, 0, 0); #0.3=30%
    }


```
</details>

## Energie
![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/10.jpg)
<details>
  <summary>Carte énergie</summary>

```yaml
type: custom:stack-in-card
mode: vertical
keep:
  box_shadow: true
  margin: true
  border_radius: true
  background: true
  outer_padding: false
cards:
  - type: vertical-stack
    cards:
      - type: energy-distribution
        link_dashboard: false
        card_mod:
          style: |
            ha-card {
              border-width: 0px !important;
              background: rgba(0, 0, 0, 0); #0.3=30%
              box-shadow: none;
              
            }
      - type: energy-date-selection
        card_mod:
          style: |
            ha-card {
              border-width: 0px !important;
              background: rgba(0, 0, 0, 0); #0.3=30%
              box-shadow: none;
              margin-right: 300px;
            }
  - type: horizontal-stack
    cards:
      - type: vertical-stack
        cards:
          - type: custom:mushroom-template-card
            primary: "Consomation et provenance :"
            card_mod:
              style: |
                ha-card {
                  border-width: 0px !important;
                  background: rgba(0, 0, 0, 0); #0.3=30%
                  box-shadow: none;
                  
                }
          - type: energy-usage-graph
            card_mod:
              style: |
                ha-card {
                  border-width: 0px !important;
                  background: rgba(0, 0, 0, 0); #0.3=30%
                  box-shadow: none;
                  

                }
      - type: vertical-stack
        cards:
          - type: custom:mushroom-template-card
            primary: "Production solaire :"
            card_mod:
              style: |
                ha-card {
                  border-width: 0px !important;
                  background: rgba(0, 0, 0, 0); #0.3=30%
                  box-shadow: none;
                  
                }
          - type: energy-solar-graph
            card_mod:
              style: |
                ha-card {
                  border-width: 0px !important;
                  background: rgba(0, 0, 0, 0); #0.3=30%
                  box-shadow: none;
                  
                }
card_mod:
  style: |
    ha-card {
      border-width: 0px !important;
      background: rgba(0, 0, 0, 0); #0.3=30%
      box-shadow: none;
    }


```
</details>

## Eau
![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/11.jpg)
<details>
  <summary>Carte eau</summary>

```yaml
type: custom:vertical-stack-in-card
cards:
  - type: custom:mushroom-template-card
    primary: "Consomation d'eau :"
    card_mod:
      style: |
        ha-card {
          border-width: 0px !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
  - type: energy-water-graph
    card_mod:
      style: |
        ha-card {
          border-width: 0px !important;
          background: rgba(0, 0, 0, 0); #0.3=30%
          box-shadow: none;
        }
card_mod:
  style: |
    ha-card {
      border-width: 0px !important;
      background: rgba(0, 0, 0, 0); #0.3=30%
      box-shadow: none;
    }


```
</details>

## Alarmo
![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/12.jpg)
<details>
  <summary>Carte alarmo</summary>

```yaml
type: custom:alarmo-card
entity: alarm_control_panel.alarmo
name: Alarme
keep_keypad_visible: false
use_clear_icon: true
button_scale_actions: 2.2
button_scale_keypad: 2.2
states:
  armed_away:
    button_label: Activer
    state_label: Activée
show_messages: true
show_ready_indicator: true
show_bypassed_sensors: true
card_mod:
  style: |
    ha-card {
      border-width: 0px !important;
      card-border-width: 0px;
      background: rgba(0, 0, 0, 0); #0.3=30%
      box-shadow: none;
    }


```
</details>

## Setup
| Matériel | Type | 
| --- | --- | 
| Raspberry |  `RaspberryPi 5 8GB` | 
| SSD |  `Seeed studio 128GB NVMe M.2 PCIe Gen3x4` | 
| Z-wave | `Aeotec Z-stick 7` |  
| Case | `Argon NEO 5 M.2 NVME` |    

## Intégrations - HACS |- Sera complété prochainement -|


  [Decluttering Card ](https://github.com/custom-cards/decluttering-card)  
  _Reuse multiple times the same card configuration with variables to declutter your config_

  [lovelace-card-mod ](https://github.com/thomasloven/lovelace-card-mod)  
  _Add CSS styles_
  
  [lovelace-layout-card ](https://github.com/thomasloven/lovelace-layout-card)  
  _Get more control over the placement of lovelace cards_
  
  [vertical-stack-in-card ](https://github.com/ofekashery/vertical-stack-in-card)  
  _To group multiple cards into a single sleek card_
  
  [button-card ](https://github.com/custom-cards/button-card)  
  _Lovelace button-card_

  [apexcharts-card](https://github.com/RomRider/apexcharts-card)  
  _Higly customizable graph card_
  
  [Lovelace Mini Graph Card](https://github.com/kalkih/mini-graph-card)  
  _Minimalistic graph card_

  [bar-card](https://github.com/custom-cards/bar-card)  
  _Customizable Animated Bar card_

  [swipe-card](https://github.com/bramkragten/swipe-card)  
  _A Lovelace card that uses swiper to create a touch slider that lets you flick through multiple cards_




# HAMR-Tablette
![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/01.jpg)
<details>
  <summary>baseyaml</summary>

```yaml


```
</details>
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

![01](https://github.com/Superpixou/HAMR-Tablette/blob/main/Images/03.jpg)

<details>
  <summary>Carte sonos</summary>

```yaml


```
</details>


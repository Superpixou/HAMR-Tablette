# HAMR-Tablette
<details>
  <summary>baseyaml</summary>

```yaml


```
</details>

![01](https://github.com/user-attachments/assets/76ffa6bc-c014-43eb-8477-94ad761a9583)
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


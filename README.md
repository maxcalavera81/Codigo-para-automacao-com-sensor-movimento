# Codigo-para-automacao-com-sensor-movimento

  - alias: Iluminação Sala 17h00-19h30
    trigger:
      platform: state
      entity_id: binary_sensor.motion_sensor_158d0001f9d417
      from: 'off'
      to: 'on'
    condition:
    - condition: time
      after: '17:00:00'
      before: '19:30:00'
    - condition: numeric_state
      entity_id: sensor.illumination_158d0001f9d417
      below: 10
    action:
      - service: light.turn_on
        entity_id: group.sala
        data:
          brightness: 255
          kelvin: 6500
      - service: light.turn_on
        data:
          entity_id: binary_sensor.motion_sensor_158d0001f9d417
      - service: light.turn_off
        entity_id: light.yeelight_rgb_7811dce0fe41
  - alias: Sala OFF 17h-19h30
    trigger:
      platform: state
      entity_id: binary_sensor.motion_sensor_158d0001f9d417
      from: 'on'
      to: 'off'
      for:
        minutes: 10
    action:
      - service: light.turn_off
        entity_id: group.sala
      - service: light.turn_off
        data:
          entity_id: binary_sensor.motion_sensor_158d0001f9d417

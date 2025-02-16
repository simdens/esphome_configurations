# esphome_configurations
Configuration files of my ESPHome devices

## stromzahler-heizung.yaml
Configuration for the Ferraris energy meter. 

I was not satisfied with the known solutions 

  * https://www.simon42.com/home-assistant-ferraris-zahler-ht-nt-tarif/

Issues with known solutions:

  * Digital output has no schmitt trigger integrated (just standard comparator)
  * time wise debouncing not reliable for Ferraris energy meter
  * bad measuring of low power with [Pulse Meter Sensor](https://esphome.io/components/sensor/pulse_meter.html)
    * Either bad resolution, i.e. low `timeout` value
    * or bad update times, i.e. high `timeout`value

### Feautures of this implementation

  * **Reliable Measurement**
  * energy meter value survives reboot
  * `stromzahler_heizung_energymeter_set_value`-Action to set energy meter value from inside Home Assistant
  * Debouncing of input signal (Schmitt Trigger on analog value)
  * Fast following on sudden power consumption drops



### Used Parts
  * ESP8266-12F D1 Mini 
  * [TRCT5000](https://www.amazon.de/AZDelivery-TRCT5000-Infrarot-Hindernis-Vermeidung/dp/B07DRCKV3X) Line Follower Module

### Hardware Setup

Connect pins according to following table

| ESP82660 | TRCT5000 |
|----------|----------|
| 3V3      | VCC      |
| Gnd      | Gnd      |
| not used | Do       |
| A0       | Ao       |


### Software Setup

Set the `kWh_per_pulse` substitution as needed.
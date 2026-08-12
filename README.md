# ESPHome Tuya Curtain (LY1998 / WBR3) Package

A reusable ESPHome package template designed for Tuya-based Wifi smart curtain motors that rely on a USB stick as RF-WIFI gateway. On my device, the LY-Gateway v1.7, a WBR3 Tuya Wifi module along with TuyaMCU is present. This package is to be used in a ESPHome generated firmware for that WBR3 MCU board. This package abstracts core UART communication, calibration state management, telemetry sensors, and configuration entities into a clean, parameterizable include file.

---

## Features

* **Parameterized Entities & IDs:** Supports multiple curtain motors on a single device or across different nodes without ID collisions by utilizing unique substitution prefixes.
* **Calibration State Machine:** Tracks calibration stages (Idle, Closed, Mapping, Complete) with automated tracking of MCU Datapoints (`DP4`, `DP102`, `DP8`).
* **Comprehensive Telemetry & Config:** Includes sensors for battery level, temperature, fault codes, work state, and configurable entities (motor reversal, temperature threshold, learning mode, default end).
* **Watchdog Monitoring:** Dedicated GPIO watchdog binary sensor support.

---

## Prerequisites & Substitutions

When including this package, you must supply the required substitution variables to map your board's physical pins and unique entity names.

| Variable Name | Description | Default Example |
| :--- | :--- | :--- |
| `cover_name` | The friendly name shown in Home Assistant for the cover. | `"Rideaux opaques"` |
| `cover_id` | Unique internal ESPHome ID for the cover component. | `id_cover_opaque` |
| `entity_name_prefix` | Prefix applied to all UI-facing entity names. | `"Curtain 1"` |
| `uart_tx_gpio` | ESP32 TX pin connected to the Tuya module. | `GPIO21` |
| `uart_rx_gpio` | ESP32 RX pin connected to the Tuya module. | `GPIO20` |
| `watchdog_pin` | GPIO pin assigned to the TuyaMCU watchdog trigger. | `GPIO10` |

---

## Installation & Usage

Add the package to your device's main ESPHome YAML configuration using the remote package loader:

```yaml
packages:
  curtain_opaque:
    url: https://github.com/bennydiamond/esphome_ly_1998_template
    ref: master
    files: 
      - path: ly1998_template.yaml
        vars:
          cover_name: "Opaque curtains"
          cover_id: id_cover_opaque
          entity_name_prefix: "Curtain 1"
          uart_tx_gpio: GPIO21
          uart_rx_gpio: GPIO20
          watchdog_pin: GPIO10
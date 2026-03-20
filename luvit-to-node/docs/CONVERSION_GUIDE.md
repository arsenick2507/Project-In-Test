# Guide de Conversion : Luvit-RED → Node-RED

## 📋 Table des Matières

1. [Architecture Générale](#architecture-générale)
2. [Modbus RTU](#modbus-rtu)
3. [LoRaWAN / UDP](#lorawanuudp)
4. [Azure IoT Hub](#azure-iot-hub)
5. [Gestion d'État](#gestion-détat)

## Architecture Générale

### Luvit-RED (CloudGate - ARM64)
\\\
CloudGate Device
├── Luvit Runtime (Lua)
├── Flow Engine (Custom)
├── Serial Port (Modbus RTU)
├── Network (LoRaWAN, UDP)
└── HTTPS Client (Azure IoT Hub)
\\\

### Node-RED (reComputer - x86)
\\\
Seeed Studio reComputer
├── Node-RED Server (Node.js)
├── Flow Engine (JSON-based)
├── Modbus Contrib (Serial RTU)
├── MQTT Client (LoRaWAN relay)
└── Azure IoT Hub Integration
\\\

## Modbus RTU

### Luvit-RED (Lua)
\\\lua
-- Serial port configuration
local port = serial.open(\"/dev/ttyUSB0\", 9600, 8, 1, 0)

-- Read holding registers (slave 1, addr 0, qty 10)
local function read_modbus()
  local query = {0x01, 0x03, 0x00, 0x00, 0x00, 0x0A, 0xXX, 0xXX}
  port:write(query)
  local response = port:read(1000)
  return parse_registers(response)
end
\\\

### Node-RED (JSON Flow)
Voir les exemples dans le dossier flows/

## Configuration Port Série
- Port : \/dev/ttyUSB0\ (ou votre port USB)
- Baud Rate : 9600
- Data Bits : 8
- Stop Bits : 1
- Parity : None

## Ressources

- [Node-RED Documentation](https://nodered.org/docs/)
- [node-red-contrib-modbus](https://flows.nodered.org/node/node-red-contrib-modbus)
- [Azure IoT Hub MQTT](https://learn.microsoft.com/en-us/azure/iot-hub/iot-hub-mqtt-support)

**Auteur** : HeX Group / Safyr Solution
**Date** : Mars 2026

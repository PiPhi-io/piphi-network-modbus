# Piphi Network Modbus

Generated PiPhi integration runtime.

## Run locally

```bash
pdm install -G dev
pdm run uvicorn piphi_network_modbus.main:app --reload --port 4222
pdm run pytest
pdm run python scripts/validate.py
```

The runtime listens on port `4222` by default and exposes the common PiPhi runtime route contract:

- `GET /health`
- `GET /diagnostics`
- `POST /discover`
- `POST /config`
- `POST /config/sync`
- `POST /deconfigure`
- `POST /deconfigure/{config_id}`
- `GET /state`
- `GET /contract`
- `GET /entities`
- `GET /events`
- `POST /events/device/{config_id}/example`
- `POST /telemetry/example`
- `POST /telemetry/device/{config_id}/example`
- `POST /command`

## Capability coverage

`capability-catalog.json` inventories Modbus transports, units, profiles,
coils, discrete inputs, registers, types, diagnostics, polling quality, and a
managed RTU gateway boundary. Each candidate is implemented, planned, or
excluded, and contract tests prevent unsupported register operations from
being advertised.

Protocol features remain planned until semantic profiles, unit/address
allow-lists, type and endian fixtures, batching, retry behavior, and safe write
tests exist. Arbitrary addresses, PDUs, broadcasts, and serial devices are
explicitly excluded.

## Manifest

`manifest.json` is a starter manifest. Before publishing, update:

- `image`
- `version`
- capabilities and commands
- config fields and identity fields
- entity metadata

## Docker

```bash
docker build -t docker.io/piphinetwork/piphi-network-modbus:0.1.0 .
docker run --rm -p 4222:4222 docker.io/piphinetwork/piphi-network-modbus:0.1.0
```

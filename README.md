# Deployment

## Google Maps API keys

For local deployment, copy `.env.example` to `.env` and set both Google Maps API
keys:

```powershell
Copy-Item .env.example .env
```

`docker compose` loads `.env` automatically when run from this directory. The
`.env` file is ignored by Git and must not be committed. For deployments through
GitHub Actions, configure the `GOOGLE_MAPS_API_KEY` and
`GOOGLE_MAPS_BROWSER_KEY`, `RABBITMQ_DEFAULT_USER`, `RABBITMQ_DEFAULT_PASS`,
and `REGISTRY_HOST` repository secrets.

The Compose stack enables RabbitMQ's MQTT plugin and exposes MQTT on port 1883.
FMS subscribes to VDA 5050 vehicle state topics and the emulator publishes
coordinates to the same broker. The emulator web page is available on port
9030; FMS remains on port 9020. Configure `VEHICLE_MANUFACTURER` and
`VEHICLE_SERIAL_NUMBER` in `.env` to match the emulator identity shown in
`uagv/v2/{manufacturer}/{serialNumber}/state`.

RabbitMQ's default user and password are only applied when its data directory
is first initialized. If `mongo`/RabbitMQ already has a persistent broker
configuration, create or update the RabbitMQ user to match the deployment
secrets before starting these services.
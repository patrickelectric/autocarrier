# autocarrier
[![ArduPilot](https://github.com/patrickelectric/autocarrier/actions/workflows/ardupilot.yml/badge.svg)](https://github.com/patrickelectric/autocarrier/actions/workflows/ardupilot.yml)
[![Linux2Rest](https://github.com/patrickelectric/autocarrier/actions/workflows/linux2rest.yml/badge.svg)](https://github.com/patrickelectric/autocarrier/actions/workflows/linux2rest.yml)
[![MAVLink2Rest](https://github.com/patrickelectric/autocarrier/actions/workflows/mavlink2rest.yml/badge.svg)](https://github.com/patrickelectric/autocarrier/actions/workflows/mavlink2rest.yml)
[![MAVProxy](https://github.com/patrickelectric/autocarrier/actions/workflows/mavproxy.yaml/badge.svg)](https://github.com/patrickelectric/autocarrier/actions/workflows/mavproxy.yaml)
[![MAVLink-Server](https://github.com/patrickelectric/autocarrier/actions/workflows/mavlink-server.yml/badge.svg)](https://github.com/patrickelectric/autocarrier/actions/workflows/mavlink-server.yml)

My personal docker container deployment environment

## Composer
- `docker compose -f compose.yml --profile ardusub --profile mavlink2rest up`
- `docker compose run mavlogdump /binded/test.tlog > potato.txt`

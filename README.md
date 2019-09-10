# Kingsly

<p align="center"><img src="docs/Kingsly.png" width="360"></p>
<p align="center">
  <a href="https://travis-ci.org/gojekfarm/kingsly"><img src="https://travis-ci.org/gojekfarm/kingsly.svg?branch=master" alt="Build Status"></img></a>
</p>

An attempt to automate SSL certs management. This Cert manager helps generate SSL certs, renews them automatically. [Release blog post](https://blog.gojekengineering.com/introducing-kingsly-the-cert-manager-ced40746aa65)

#### Assumptions

- The FQDN points to a public IP address
- An FQDN points to only one IP address

## Dev Setup

#### Install docker-compose

If you're on OS X, please follow the instructions to install [docker](https://docs.docker.com/docker-for-mac/install/).
Or if you're on a Unix based distribution, you can follow the instructions [here](https://docs.docker.com/compose/install/) to install docker-compose.

```
# For Linux based machines
$ sudo curl -L "https://github.com/docker/compose/releases/download/1.24.0/docker-compose-$(uname -s)-$(uname -m)" -o /usr/local/bin/docker-
$ sudo chmod +x /usr/local/bin/docker-compose
```

- Run `$ make .env` to create `.env` for the application from `.env.sample`

#### Opening the web interface on your dev machine

```
$ make docker.start
```

You can then open `localhost:8080`

#### To stop the docker containers

```
$ make docker.stop
```

#### Running the specs

```
$ make rspec
```

## Example APIs

- Creating SSL certs for a domain:
  - Request:
```
curl -X POST http://kingsly.host/v1/cert_bundles \
  -u admin:password \
  -H 'Content-Type: application/json' \
  -d '{
        "top_level_domain":"your-domain.com",
        "sub_domain": "your-sub-domain"
    }'
```
  - Response:

```
'{
  "private_key":"-----BEGIN RSA PRIVATE KEY-----\nFOO...\n-----END RSA PRIVATE KEY-----\n",
  "full_chain":"-----BEGIN CERTIFICATE-----\nBAR...\n-----END CERTIFICATE-----\n"
}'
```

## Deploying

Please refer to [deployment](https://github.com/gojekfarm/kingsly/tree/master/docs) docs here 

## TODO

- check for ACME account creation without email id (maybe initialize account only once?)
- tracks if the client has the updated cert  (WIP: [#5](https://github.com/gojekfarm/kingsly/issues/5))

## License

```
Copyright 2018, GO-JEK Tech <http://gojek.tech>

Licensed under the Apache License, Version 2.0 (the "License");
you may not use this file except in compliance with the License.
You may obtain a copy of the License at

    http://www.apache.org/licenses/LICENSE-2.0

Unless required by applicable law or agreed to in writing, software
distributed under the License is distributed on an "AS IS" BASIS,
WITHOUT WARRANTIES OR CONDITIONS OF ANY KIND, either express or implied.
See the License for the specific language governing permissions and
limitations under the License.
```

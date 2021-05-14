# containered dhcp
DHCP in a container, based on dnsmasq.

## usage
Adjust the dnsmasq.conf according to your needs and run one of the following methods.

### docker run
`docker run --cap_add=NET_ADMIN -p <bindip>:67:67/udp -p <bindip>:67:67/tcp -v $PWD/containerdata:/container thetillhoff/dhcp`

- `--cap_add=NET_ADMIN` required to use port 67
- `-p <bindip>:67:67/[udp|tcp]` forward port 67 with both protocols to container

### docker-compose
```
version: '3.8'
services:
  dns:
    image: thetillhoff/dhcp
    capabilites:
      add: ["NET_ADMIN"]
    ports:
      - "<bindip>:67:67/udp"
      - "<bindip>:67:67/tcp"
    volumes:
      - "$PWD/containerdata:/container"
```

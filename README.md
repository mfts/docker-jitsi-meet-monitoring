
# Jitsi (Video Bridge) Monitoring
> [Jitsi](https://jitsi.org/what-is-jitsi/) = Open source project for secure video conferencing solutions. \
> [Jitsi Video Bridge](https://github.com/jitsi/jitsi-videobridge) = Video router for WebRTC.

## Job Checklist
- [x] REST
- [ ] XMPP MUC

## Jitsi Statistics Documentation
- https://github.com/jitsi/jitsi-videobridge/blob/master/doc/statistics.md

## How to Try
1. Ensure that Docker and Docker-Compose are installed. \
[How to Install Docker](https://docs.docker.com/get-docker/) and [How to Install Docker-Compose](https://docs.docker.com/compose/install/)
2. This repo clone
    ```
      $ git clone https://github.com/mfts/docker-jitsi-meet-monitoring.git
    ```
3. Start docker-compose
    ```
      $ docker-compose up -d
    ```
4. Open Grafana at http: // localhost: 3000
5. Create a data source to InfluxDB \
The username and password can be seen in the `.env` file
6. Import the Dashboard from the file `fixtures/grafana-dashboard.json`
7. Configuring Jitsi Video Bridge (JVB)
  - `videobridge/config` file
    ```
      # extra options to pass to the JVB daemon
      JVB_OPTS = "- apis = rest"
    ```
  - `videobridge/sip-communicator.properties` file
    ```
      # Additional Configuration
      org.jitsi.videobridge.rest.private.jetty.port = 8080
      org.jitsi.videobridge.ENABLE_STATISTICS = true
      org.jitsi.videobridge.STATISTICS_TRANSPORT = colibri
    ```
8. Change the telegraph configuration according to the JVB component you want to monitor \
Example:
    ```
      ...
      ## List of urls to query.
      urls = ["http://meet.example.com:8080/about/health"]
      ...
      ## URL of each server in the service's cluster
      urls = [
        "http://meet.example.com:8080/colibri/stats",
      ]
      ...
    ```

### Image Snapshot
![Grafana-JVB](https://raw.githubusercontent.com/mfts/docker-jitsi-meet-monitoring/master/img/grafana-dashboard.png "Grafana Dashboard")

## Credits
1. InfluxData
2. Grafana Labs
3. Jitsi

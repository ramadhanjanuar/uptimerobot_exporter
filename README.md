# uptimerobot.com prometheus exporter

Exports all your uptimerobot.com checks for prometheus scraping,
so you can use external, third-party checks in your monitoring setup.

*Caveat: This does not (yet) handle paging, so if you have a Pro account
with uptimerobot.com you might have more checks defined than this script
will handle.*

If you do not have a pro account, any scrape interval shorter than
`scrape_interval: 5m` for this exporter will a) produce duplicated data
and b) misuse uptimerobots API.

## Requirements

* Python
* [requests](http://www.python-requests.org/en/master/)

## Running

Accepted parameters:

* api_key: Your uptimerobot.com API key. See section 'API Settings' in [your account details](https://uptimerobot.com/dashboard#mySettings).
* server_name (optional): Name to bind the HTTP server to. Default: 0.0.0.0
* server_port (optional): Port to bind the HTTP server to. Default: 9705

You can either pass script arguments (run `python exporter.py -h` for an explanation)
or set the following environment variables:

* `UPTIMEROBOT_API_KEY`
* `UPTIMEROBOT_SERVER_NAME`
* `UPTIMEROBOT_SERVER_PORT`

## Docker

Run `docker run -e 'UPTIMEROBOT_API_KEY=...' -p 9705:9705 --read-only hnrd/uptimerobot_exporter`.

## docker-compose

Example compose file:

    version: '2.1'
    
    services:
      exporter:
        image: hnrd/uptimerobot_exporter
        restart: unless-stopped
        environment:
          UPTIMEROBOT_API_KEY: u123456-1a2b3c4d5e6f7890abc12323
        ports:
          - 9705:9705
        read_only: true
    


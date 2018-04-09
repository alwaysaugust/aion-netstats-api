AION netstats API
============

This is Cubedro's [eth-net-intelligence-api](https://github.com/cubedro/eth-net-intelligence-api) with a
few modifications.

This is the backend service which runs along with AION and tracks the network status, fetches information through JSON-RPC and connects through WebSockets to (http://aionstats.com) to feed information.


## Prerequisite
* AION
* node
* npm

## Installation

Clone the repository and install the dependencies

```bash
git clone https://github.com/alwaysaugust/aion-netstats-api
cd aion-netstats-api
npm install
sudo npm install -g pm2
```

## Configuration

Configure the app modifying app.json.

- alter the value to the right of LISTENING_PORT to the AION listening port (default: 30303)
- alter the value to the right of INSTANCE_NAME to whatever you wish to name your node;
- alter the value to the right of CONTACT_DETAILS if you wish to share your contact details
- alter the value to the right of RPC_PORT to the rpc port for your node (by default 8545 for both cpp and go);
- and alter the value to the right of WS_SECRET to the secret

```json
"env":
	{
		"NODE_ENV"        : "production", // tell the client we're in production environment
		"RPC_HOST"        : "localhost", // aion JSON-RPC host
		"RPC_PORT"        : "8545", // aion JSON-RPC port
		"LISTENING_PORT"  : "30303", // aion listening port (only used for display)
		"INSTANCE_NAME"   : "", // whatever you wish to name your node
		"CONTACT_DETAILS" : "", // add your contact details here if you wish (email/skype)
		"WS_SERVER"       : "wss://rpc.aionstats.com", // path to aion-stats WebSockets api server
		"WS_SECRET"       : "", // WebSockets api server secret used for login
		"VERBOSITY"       : 2 // Set the verbosity (0 = silent, 1 = error, warn, 2 = error, warn, info, success, 3 = all logs)
	}
```
## Run

AION must be running.

Enable the network apis by adding 'net' to the list of enabled apis in your cofing.xml file

'<apis-enabled>web3,eth,personal,net</apis-enabled>'

Run the process with:
```bash
pm2 start app.json
```
PM2 commands:

'pm2 list' to display the process status;
'pm2 logs' to display logs;
'pm2 gracefulReload node-app' for a soft reload;
'pm2 stop' node-app to stop the app;
'pm2 kill' to kill the daemon.

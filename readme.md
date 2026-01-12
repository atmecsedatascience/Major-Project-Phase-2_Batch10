# Pipechime:   Data Analytical CLI with flwr

<p align="center">
  <a href="https://github.com/vignexshh/pipechime">
    <img src="read-images/pipechime_16_9_banner.png" width="1000px" alt="Pipechime Banner Image" />
  </a>
</p>  



Pipechime (`pchime`) is a CLI package used to perform federated based machine learning centric data analytics with the help of [flwr](https://github.com/adap/flower), [pandas](https://github.com/pandas-dev/pandas) and python based ml frameworks.

### Developer Notes

Pipechime is an ongoing project and is currently staged precautiously for experimentation purpose only. Model performance can only be determined only while comparing with centralised learning.

### Roadmap

Pchime is focused on creating easy to use CLI that could further support to GUI centric application integrations. The below figure represents the current state that only utilises `server-client` architecture with example banking specific scenario

<img src="read-images/pipeChime_server_arch.png" width="500px"  alt="Pipechime server-client architecture Image" />

Our further plans are determined to have `only-clients` (gossip) architecture 
<img src="read-images/pipechime_app_architecture.drawio.png" width="500px"  alt="Pipechime server-client architecture Image" />


## Installation & Usage 

### Installaing pchime from github repository
[⚠️] : It's recommended to use python virtual environments for each instance to prevent version mismatch errors. 

#### 1. Clone the repository

- `https://github.com/vignexshh/pipechime.git` 
- **Or** with Github CLI `gh repo clone vignexshh/pipechime`
#### 2. Install package  from github
- `cd pipechime` **or** change directory where you have cloned current repository
- `pip install e .`
##### with pip
- `pip install pchime` 
#### 3. Recommended to export the installation directory to PATH. 
- `export PATH=$PATH:/path/to/your/directory`
- validate the operation with `echo $PATH`

### Usasge with pchime CLI 
- Loading new tabular data as `.parquet`  from federated client side:
`pchime load --<tabular_data_file_extention> --project <path/to/partitioned/file>`

- Initiating a device as server:
`pchime server --start <server_device_address:port> --federatedRounds <INT> --n_count <client count> --outDirectory <path/to/save/npz/outputs>`

- Computing with client and sending parameters to server (Under  same network as server):
`pchime client --start <server_device_address:port> --project <project_name or path/to/paritioned/data>`

### Networking
- To Compute between 2 distinct and distant remote networks, you need to configure firewall inbound rules in server machine and route tcp traffic to pass by your router. 
- If the above mentioned steps seems complicated and hard, just tcp forward your local ip add + port with [ngrok](https://ngrok.com/docs/universal-gateway/tcp) using
`ngrok tcp <port>` 
- Then use the returned tcp ip address when ngrok has started. e.g. `tcp://0.tcp.in.ngrok.io:<XXXX> -> localhost:8080 `
- Strip the leading `tcp://` and use as
- `pchime client --start 0.tcp.in.ngrok.io:<1111> --project <project_name or path/to/paritioned/data>`






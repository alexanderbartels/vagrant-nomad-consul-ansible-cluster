# vagrant-nomad-consul-ansible-cluster

its like https://github.com/nickvth/ansible-consul-nomad but with 3 centOS nodes


TODO:

# nomad cli
it needs the ```NOMAD_ADDR``` environment variable set to
```export NOMAD_ADDR=http://nomad-server.service.consul:4646```

# consul cli
it needs the ```CONSUL_RPC_ADDR```environment variable set to
```export CONSUL_RPC_ADDR=<IP>:8400```
```export CONSUL_RPC_ADDR=192.168.33.10:8400```

or the hostname, configured in /etc/hosts (different on every machine)
```export CONSUL_RPC_ADDR=control-01:8400```



-------

1.) Start the nginx job.

-> show ```docker ps```to get the address and port.

-> Beide Adressen öffnen.

-> ```docker kill <CONTAINER_ID>```, zeigen das ein Dienst automatisch neu gestartet wird.

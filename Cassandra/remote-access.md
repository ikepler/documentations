## Remote Access to Cassandra :desktop_computer:

To enable remote access to the Cassandra, you should bind an address to the Cassandra service and enable its RPC. For this purpose, you can follow these steps:

1. Open `/etc/cassandra/cassandra.yaml` configurations file.
2. Find `listen_address`, uncomment it with removing the heading `#` and put your valid address there. After this it must be like `listen_address: xxx.xxx.xxx.xxx`.
3. Find `broadcast_address` and put the broadcast address ahead of it. IT could be your localhost address if your nodes are just on a server, or your master node address. On case of leaving it, it takes the `listen_address` value.
4. Find `start_rpc` and set its value to `true`.
5. Find `rpc_port` and change it if you need.
6. Find `broadcast_rpc_address` and fill it based on items 2 and 3.
7. Find `seed_provider` and look on it for `seeds` item. Append the address from previous items on it. It should like this:

    ```yaml
    seed_provider:
        - class_name: org.apache.cassandra.locator.SimpleSeedProvider
          parameters:
              - seeds: "127.0.0.1,xxx.xxx.xxx.xxx"
    ```

8. Restart the Cassandra service!
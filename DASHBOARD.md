# Creating the web dashboards based on GrimoireLab

If you want to create from scratch the web dashboards instead of using the online version, you need to use GrimoireLab.

In order execute GrimoireLab to generate the web dashboards, you can use the docker-compose included in the folder conf. You need:

* A [Git](https://git-scm.com/) client to download the repo
* [Docker Engine](https://docs.docker.com/install/) and [Docker Compose](https://docs.docker.com/compose/install/)
* At least, 2CPUs, 8GB memory RAM, and 2GB SWAP (MacOS users can manage it with [Docker client for Mac](https://hub.docker.com/editions/community/docker-ce-desktop-mac))
* The port 3306 to be free/not used by other processes
* [Enough virtual memory for Elasticsearch](https://www.elastic.co/guide/en/elasticsearch/reference/current/vm-max-map-count.html). You can do it running the following command as `root` in Linux or as administrator user in MacOS:

  * Linux
    ```console
    sysctl -w vm.max_map_count=262144
    ```

  * Mac
    ```
    $ screen ~/Library/Containers/com.docker.docker/Data/vms/0/tty
    (then run:) sysctl -w vm.max_map_count=262144
    ```

    Remember also to assign proper resources to Docker through the UI. 8GB Memory and 2GB Swap should work.

## Steps

- Clone the repo:
    ```console
    git clone https://github.com/aylabs/iotfloss
    ```
- Cd to the conf directory
    ```console
    cd iotfloss/conf
    ```

- Add one or more GitHub API tokens in the setup.cfg as follows:
   ```
   [github]
    ...
    api-token = token
    ...
   ```
   or
   ```
   [github]
    ...
    api-token = [token-1, token-2]
    ...
   ```

- Start the docker-compose:
    ```console
    docker-compose up -d
    ```

If everything goes well, data will be gathered and processed. To get access to
them, go to `http://localhost:5601`

### FAQ

**- How to get a GitHub API token?**

https://help.github.com/en/articles/creating-a-personal-access-token-for-the-command-line.

**- How to add/remove repositories?**

Repositories can be added (or removed) by modifying the projects.json. More information about this file is available
at https://github.com/chaoss/grimoirelab-sirmordred#projectsjson).

**- How to restart GrimoireLab after adding new repositories to the projects.json?**

```console
docker-compose restart
```

**- How to redeploy GrimoireLab from scratch?**

```console
docker-compose down && docker-compose up -d
```

**- How to manage contributors profile?**

To manage contributors profile information with [HatStall](https://github.com/chaoss/grimoirelab-hatstall),
go to `http://localhost:8000`. To get access:
* User: `admin`
* Pass: `admin`

You can change user and password in the `docker-compose.yml` file.
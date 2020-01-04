# IoT Projects in FLOSS Foundations

In the last decade, Industry 4.0 has emerged as a revolution for the traditional technology, and the Internet of Things (IoT) is at the core of it. Apache, Eclipse and Linux foundations, three of the main actors in Open Source, have put in place their own IoT architectures powered by different Open Source projects. In this talk, these architectures are compared and a common architecture is identified based on emerging standards, with a special focus in the Edge. Then, the common architecture is used to classify the different Open Source projects.
 
For each project, activity and community analysis based on the data extracted from Git and Github issue trackers is achieved using the GrimoireLab platform, a powerful Open Source tool for software analytics. Finally, the data obtained is used to understand the Open Source IoT landscape in terms of companies involved, leading projects, technologies adopted and communities.
 
More than 50 projects have been analyzed and all of them are classified in the categories: Edge, Cloud, Enterprise, Tools. And inside the Edge category, five subcategories are defined: OS and virtualization in devices, communication protocols, data processing, platforms for interoperability and applications. For all the projects the data for the activity (commits) and community size (people doing commits) are extracted and analyzed in time series.
 
The data will be presented as dashboards that all attendees can consult online and all the data could be shared with interested people for further analysis.

# Run GrimoireLab

In order execute GrimoireLab, you can use the docker-compose included in the folder conf. You need:

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
title: Cassandra and Docker – round 1
date: 2014-09-18
slug: /2014/09/18/cassandra-and-docker-round-1/
tags: Cassandra, Docker, cassandra, docker, tutorial

[<img class="aligncenter size-medium wp-image-340" src="http://ivan.pedrazas.me/wp-content/uploads/2014/09/Cassandra_logo.svg_-300x201.png" alt="Cassandra_logo.svg" width="300" height="201" />][1]

&nbsp;

This last week I&#8217;ve spent some time trying to set up Cassandra in Docker. My starting point was this Docker Image called [pokle/cassandra][2].

There are things from that image that I don&#8217;t like and I&#8217;ve been very tempeted to fork it, but as I said, it was a starting point, and for what we need now, it&#8217;s good enough.

Basically what I wanted was to have a cluster of 3 machines running in Docker, talking to each other and letting me &#8220;play away&#8221;.

I&#8217;m re-writing dotMarks in java using Dropwizard and, of course, Cassandra. Anyway, this post is about how to set up that cluster.

Open your terminal and paste this:

<pre># Make dirs to store your data
sudo mkdir -p /data/cassandra/{c1,c2,c3}/data
sudo mkdir -p /data/cassandra/{c1,c2,c3}/commitlog

# Change permissions so the Cassandra user can write on them
sudo chmod 777 /data/cassandra/{c1,c2,c3}/data
sudo chmod 777 /data/cassandra/{c1,c2,c3}/commitlog

# Run the Docker containers with Cassandra
docker run -d --name c1 -v /data/cassandra/c1/data:/var/lib/cassandra/data -v /data/cassandra/c1/commitlog:/var/lib/cassandra/commitlog poklet/cassandra
docker run -d --name c2 -v /data/cassandra/c2/data:/var/lib/cassandra/data -v /data/cassandra/c2/commitlog:/var/lib/cassandra/commitlog poklet/cassandra start $(./scripts/ipof.sh c1)
docker run -d --name c3 -v /data/cassandra/c3/data:/var/lib/cassandra/data -v /data/cassandra/c3/commitlog:/var/lib/cassandra/commitlog poklet/cassandra start $(./scripts/ipof.sh c1)

# Open a CQLSH console
docker run -it --rm --link c1:c1 -v /data/cassandra/scripts:/data poklet/cassandra bash -c 'cqlsh $C1_PORT_9160_TCP_ADDR'

</pre>

Now you should have a C* cluster of 3 containers. Run docker ps and you should see something like this:

&nbsp;

<pre>-&gt; % docker ps
CONTAINER ID        IMAGE                     COMMAND               CREATED              STATUS              PORTS                                                                           NAMES
f85542cb46e3        poklet/cassandra:latest   "start 172.17.0.14"   About a minute ago   Up About a minute   8012/tcp, 9042/tcp, 9160/tcp, 22/tcp, 61621/tcp, 7000/tcp, 7001/tcp, 7199/tcp   c3                  
9cfdccaf1213        poklet/cassandra:latest   "start 172.17.0.14"   About a minute ago   Up About a minute   9160/tcp, 22/tcp, 61621/tcp, 7000/tcp, 7001/tcp, 7199/tcp, 8012/tcp, 9042/tcp   c2                  
162c36a8b876        poklet/cassandra:latest   "/bin/sh -c start"    2 minutes ago        Up 2 minutes        9042/tcp, 9160/tcp, 22/tcp, 61621/tcp, 7000/tcp, 7001/tcp, 7199/tcp, 8012/tcp   c1    
</pre>

Now, you might want to add some data. We do that using another container that will execute _**CQLSH**_.

<pre>docker run -it --rm --link c1:c1 -v /data/cassandra/scripts:/data poklet/cassandra bash -c 'cqlsh $C1_PORT_9160_TCP_ADDR'
</pre>

Note that by using Links you don&#8217;t need to know the IPs of the nodes. We will need them to connect if we don&#8217;t use a container with links, but let&#8217;s see that problem later.

Once you are in the CQLSH, add some data:

<pre>CREATE KEYSPACE dotmarks WITH REPLICATION =
 {'class': 'SimpleStrategy', 'replication_factor': 1};

 USE dotmarks;

 CREATE TABLE test_table (
  id text,
  test_value text,
  PRIMARY KEY (id)
 );


INSERT INTO test_table (id, test_value) VALUES ('1', 'one');
INSERT INTO test_table (id, test_value) VALUES ('2', 'two');
INSERT INTO test_table (id, test_value) VALUES ('3', 'three');

SELECT * FROM test_table;
</pre>

If you want to check the data from a different node, do this:

<pre>docker run -it --rm --link c2:c2 -v /data/cassandra/scripts:/data poklet/cassandra bash -c 'cqlsh $C2_PORT_9160_TCP_ADDR'


Connected to Test Cluster at 172.17.0.15:9160.
[cqlsh 4.1.1 | Cassandra 2.0.9 | CQL spec 3.1.1 | Thrift protocol 19.39.0]
Use HELP for help.
cqlsh&gt; use dotmarks;
cqlsh:dotmarks&gt; select * from test_table;

 id | test_value
----+------------
  3 |      three
  2 |        two
  1 |        one

(3 rows)

cqlsh:dotmarks&gt; 
</pre>

With this, we have our cluster ready to rock and roll! In the next post, we will see how to confdigure and connect our Dropwizard App to our Cassandra cluster.

 [1]: http://ivan.pedrazas.me/wp-content/uploads/2014/09/Cassandra_logo.svg_.png
 [2]: https://registry.hub.docker.com/u/poklet/cassandra/

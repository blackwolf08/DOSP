# COP5615 Assignment - Project 2

## Gossip and Push-Sum Algorithm on different Network Topologies

### Group Members: 

Sunny Dhama, UFID: 4328-6076, sunny.dhama@ufl.edu
Jagannath Jayanti, UFID: 1856-7125, jjayanti@ufl.edu

---

## Main Supervisor file location:

`project2/main_sup.erl`

---

## Usage

1.  cd to the `project2` folder
2.  Run erlang console

```bash
erl
```

2.  Compile all the required files

```md
c(main_sup). --> Supervisor for main actors, entry point to project
c(gs_driver_serv). --> Driver actor for gossip, this file initiates & terminates gossip algorithm
c(gs_node_supervisor). --> Supervisor for gossip nodes
c(gs_worker). --> Actor for gossip
c(ps_driver_serv). --> Driver file for push-sum
c(ps_node_supervisor). --> Supervisor for push-sum nodes
c(ps_worker). --> Actor for push-sum
c(topology_serv). --> Supervisor for topology
c(topo). --> Topology helper file

```

3.  Run
`numNodes` -> Number of nodes to run algorithm on.

`topology` -> Which topology to run algorithm on, it can be either `"line"`, `"full"`, `"2D"` and `"imp3D"`

`algorithm` -> `gossip` or `pushsum`.

```bash
erl -noshell -s main_sup start [numNodes] [topology] [algorithm]
```

examples :-

```bash
erl -noshell -s main_sup start 10000 line gossip 
erl -noshell -s main_sup start 10000 imp3D pushsum 
```

## What is Working ?

In the project, all the required topoligies i.e, `"line"`, `"full"`, `"2D"` and `"imp3D"` are successfully implemented with both the algorithms - `"gossip"` and `"pushsum"`. In both the algorithms, convergence was obtained for all the nodes. 

### Convergence for each algorithm

1. Gossip Algorithm - The network is said to converge in gossip algorithm when each node of the network has converged. Subsequently, a node converges when it hears or receives the message 10 times. Once a node converges it stops sending or transmitting the messages forwared. 

2. Push-Sum Algorithm - In a network following the push-sum protocol, each node/actor converges when it's s/w ratio does not change more than 10^-10 for 3 consecutive times the actor recieves and updates it s and w values.


## What is the largest network you managed to deal with for each type of topology and algorithm?

| Topology | Gossip | Push Sum |
| -------- | ------ | -------- |
| line     | 10,000 | 1,000     |
| full     | 8,000  | 2,500     |
| 2D       | 10,000 | 5,000     |
| imp3D    | 10,000 | 5,000     |


### Output for highest values

For implementing the project, a hierarchical design approach was followed. The main component of the system is the supervisor under which the other modules are created, each responsible for one aspect of the network. These are as follows:

- Main Supervisor (having driver server, node supervisor and topology server as children)
- Driver
- Node Supervisor
- Nodes
- Topologies


#### Input

For Gossip with line topology

```bash
erl -noshell -s main_sup start 10000 line gossip 

&& erl -noshell-s main_sup start 8000 full gossip 

&& erl -noshell-s main_sup start 10000 2D gossip 

&& erl -noshell -s main_sup start 10000 imp3D gossip
```


#### Output

##### Gossip Algorithm
```bash
-------- BEGIN gossip --------
NumNodes:'10000', Topology: line, Algorithm: gossip
Time for convergence: 673ms
-------- END gossip --------

-------- BEGIN gossip --------
NumNodes: '8000', Topology: full, Algorithm: gossip
Time for convergence: 6096ms
-------- END gossip --------

-------- BEGIN gossip --------
NumNodes:'10000', Topology: '2D', Algorithm: gossip
Time for convergence: 870ms
-------- END gossip --------

-------- BEGIN gossip --------
NumNodes:'10000', Topology: imp3D, Algorithm: gossip
Time for convergence: 3051ms
-------- END gossip --------
```

#### Input
For Gossip with line topology

```bash
erl -noshell -s main_sup start 1000 line pushsum 

&& erl -noshell-s main_sup start 1500 full pushsum 

&& erl -noshell-s main_sup start 2500 2D pushsum 

&& erl -noshell -s main_sup start 2500 imp3D pushsum
```


##### Pushsum Algorithm
```bash
-------- BEGIN pushsum --------
NumNodes: '1000', Topology: line, Algorithm: pushsum
Time for convergence: 200587ms
-------- END "pushsum" --------

-------- BEGIN pushsum --------
NumNodes: '1500', Topology: full, Algorithm: pushsum
Time for convergence: 337908ms
-------- END "pushsum" --------

-------- BEGIN pushsum --------
NumNodes: '2500', Topology: '2D', Algorithm: pushsum
Time for convergence: 256669ms
-------- END "pushsum" --------

-------- BEGIN pushsum --------
NumNodes: '2500', Topology: imp3D, Algorithm: pushsum
Time for convergence: 3014ms
-------- END "pushsum" --------
```

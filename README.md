# Modelling the coffee shop II

I have now shown you most of what I used to produce my report on the coffee shop using queueing tool.  The one final thing that you need to know is how to setup the transition rates so that 30% of agents go to the tea queue and 70% of agents go to the coffee queue.  Setting up these transition probabilities is easy.  You just need to use the commands below as follows:

```python
# Setup the queue network using the variables that you have set earlier in the code
qn = qt.QueueNetwork( g=g, q_classes=q_classes, q_args=q_args )
# Setup the transition matrix -- this is how you ensure the the ratio of agents getting coffee to agents getting tea is 7:3
qn.set_transitions( transitions )
# Tell queuing tool that only edges of type 1 get arrivals from outside the network
qn.initialize(edge_type=1)
# Tell queuing tool that you want to collect data
qn.start_collecting_data()
# Simulate the queue
qn.simulate(t=oneday)
```

The key command here is `qn.set_transitions`.  To understand how this command works, suppose that you have setup your adjacency graph as follows:

```python
adj_graph = { 0: [2], 1: [2,3], 2: [0,1,2,4], 3: [1], 4: [2], }
```

You can then set the variable called `transitions` that is passed to `qn.set_transitions` as follows:

```python
transitions = {
  0: {2: 1.0},
  1: {2: 0.3, 3: 0.7},
  2: {0: 0.20, 1: 0.3, 2: 0.25, 4: 0.25},
  3: {1: 1.0},
  4: {2: 1.0}
}
```

The probablity that an agent transitions from node 1 to node 2 is then 0.3.  Similarly the probablity that an agent transitions from node 2 to node 0 is 0.2.

You now know everything that you need to know in order to simulate the complicated network of queues that I simulated in my report and that is illustrated below:

![](coffee-shop.png)

__Your task is thus to use everything that you have learned by completing these exercises to simulate this system of queues.__  To pass the exercise you need to name the queuing tool object for simulating the queues `qt`.  Furhtermore, you must create a list called `times` that contains the total time that each agent spent within the network to get their drink.   

IoV+UAV+RSU+Cloud Task Offloading Simulation with MFO
Overview

This repository contains a simulation framework for task allocation and scheduling in a hybrid Internet of Vehicles (IoV), Unmanned Aerial Vehicles (UAVs), Road-Side Units (RSUs), and Cloud environment. The goal is to optimize task offloading and resource usage under mobility-aware conditions using the Moth-Flame Optimization (MFO) algorithm.

The system considers dynamic vehicle and UAV positions, heterogeneous resources across vehicles, UAVs, RSUs, and Cloud, and evaluates performance based on multiple metrics including task delay, load balancing, network cost, trust, and energy consumption.

System Components

Vehicles (IoV Nodes)

Randomly positioned on the road.

Each vehicle has a set of computational resources (CPU units) and a trust factor.

Vehicles move with a random speed and direction to simulate mobility.

UAVs

Fly over the road area with random positions and speed.

Provide computational resources and limited connection windows.

Also have a trust factor.

RSUs (Road-Side Units)

Fixed infrastructure along the road.

Provide relatively larger computational resources and high trust.

Cloud

Centralized resource node with abundant computing power and maximum trust.

Acts as a fallback for tasks that cannot be processed locally.

Tasks

Synthetic task dataset is generated with attributes: size (computational requirement), data (communication payload), deadline, and priority.

Each task originates from a vehicle and can be offloaded to any node type (Vehicle, UAV, RSU, Cloud).

Functions
initializeSystem(numVehicles,numUAVs,numRSUs,road_length,road_width)

Initializes all system nodes (Vehicles, UAVs, RSUs, Cloud) with random positions, resources, speed, and trust factors.

generateTasks(numTasks,Vehicles,UAVs,RSUs,Cloud)

Generates synthetic tasks with randomized size, data, deadline, and priority for the simulation.

fitnessMobilityAware(X, Tasks, Vehicles, UAVs, RSUs, Cloud)

Mobility-aware fitness function that evaluates a given task allocation X under current positions of vehicles and UAVs. It calculates a weighted sum of:

Total task delay

Network cost (data transmitted)

Load balancing across nodes

Trust of nodes

Remaining energy of nodes

computeMetricsMobility(X, Tasks, Vehicles, UAVs, RSUs, Cloud)

Computes detailed metrics for a task allocation, including total delay, load balancing (standard deviation of node loads), network cost, average trust, and remaining energy.

distanceTaskNodeMobility(task,Vehicles,UAVs,RSUs,Cloud,nodeType,nodeIdx)

Calculates Euclidean distance between the source vehicle of a task and the assigned node, taking mobility into account.

MFO_IoV(N, Max_iter, lb, ub, dim, fobj)

Implements the Moth-Flame Optimization (MFO) algorithm for solving the task allocation problem.

N is the number of moths (search agents).

Max_iter is the maximum number of iterations.

lb and ub are lower and upper bounds for task allocation (1=Vehicle, 2=UAV, 3=RSU, 4=Cloud).

fobj is the fitness function handle.

The function returns the best fitness value, best allocation of tasks, and the convergence curve.

Simulation Flow

Initialize the system nodes (Vehicles, UAVs, RSUs, Cloud).

Generate synthetic tasks for simulation.

Apply MFO to find the optimal task allocation under mobility-aware conditions.

Compute and display final evaluation metrics: total delay, load balancing, network cost, trust, and remaining energy.

Plot convergence curve of MFO.

Requirements

MATLAB R2015b or higher (compatible with later versions)

No external toolboxes required

This framework is useful for researchers and developers working on task offloading in vehicular networks, UAV-assisted computing, and cloud-edge resource management, and can be extended to test other metaheuristic algorithms.

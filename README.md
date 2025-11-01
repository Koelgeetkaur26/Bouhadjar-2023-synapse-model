# Bouhadjar-2023-synapse-model

This project is a Python simulation comparing two synapse models (Analog vs Binary) based on the 2023 paper: "Sequence learning in a spiking neuronal network with memristive synapses" (Bouhadjar et al.).

**Project Overview**

This notebook implements and simulates the core concepts from the 2023 paper. The paper explores how memristive synapses can be used for on-chip, brain-inspired sequence learning. A key challenge in neuromorphic hardware is endurance and energy consumption: memristive devices can "wear out" after too many physical write operations.

This simulation aims to quantify the hardware costs (energy and write endurance) of two different STDP learning architectures presented in the paper.

The Two Models

The paper investigates two different synapse architectures to solve this, which we simulate and compare:

- The Analog Model: This is a "write-on-every-event" model, corresponding to the paper's Analog Synapse (Eq. 1). It performs a small, gradual, physical write (and consumes energy) for every single STDP learning event (-1 on pre-spike, +5 on post-spike match). This is functionally simple but leads to massive write counts and high energy use, which is unsustainable for real hardware.

- The Binary Model: This is the paper's "smart," hardware-friendly solution, corresponding to the Binary Synapse (Eq. 2 & 3). It uses a "virtual notepad" (which the paper calls Permanence, P) to track learning events in low-power digital logic. A high-energy "physical write" is only committed once this virtual value crosses a set threshold (e.g., P > 10). This is extremely energy and endurance efficient but requires slightly more complex digital "controller" logic.

**Goal of this Simulation**

The purpose of this simulation is to implement both models and run them through the same A->B->C sequence learning task for 50 episodes. We will then compare their:

- Learning Accuracy: Do both models successfully learn the sequence?

- Hardware Cost: What is the final, total cost in physical writes (endurance) and energy consumption (pJ) for each model?

This comparison will allow us to quantify the efficiency gains of the "virtual notepad" (WSB) approach.

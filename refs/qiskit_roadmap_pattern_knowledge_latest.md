
# Introduction to Qiskit patterns

A Qiskit pattern is a general framework for breaking down domain-specific problems and contextualizing required capabilities in stages. This allows for the seamless composability of new capabilities developed by IBM Quantum™ researchers (and others) and enables a future in which quantum computing tasks are performed by powerful heterogenous (CPU/GPU/QPU) computing infrastructure. Blocks or groups of blocks perform the steps of a pattern, with the Qiskit SDK providing an important foundational layer, supported by other tools or services developed by IBM Quantum or the quantum open-source community. Qiskit patterns allow domain experts to specify a problem and compose the tooling (blocks) that achieves a Qiskit pattern. That pattern can then be executed locally, through cloud services, or deployed with Qiskit Serverless.



## The four steps of a Qiskit pattern are as follows:

- [Map problem to quantum circuits and operators](https://docs.quantum.ibm.com/guides/map-problem-to-circuits)
- [Optimize for target hardware](https://docs.quantum.ibm.com/guides/optimize-for-hardware)
- [Execute on target hardware](https://docs.quantum.ibm.com/guides/execute-on-hardware)
- [Post-process results](https://docs.quantum.ibm.com/guides/post-process-results)


![](https://docs.quantum.ibm.com/images/qiskit-patterns/patterns.svg)

Each step is detailed in the sections below.
## Map problem to quantum circuits and operators

This step describes how a user starts with a classical problem and figures out how to map it to a quantum computer. For example, in applications such as chemistry and quantum simulation, this step generally involves constructing a quantum circuit representing the Hamiltonian you are attempting to solve. During this step, for certain problems, it might also be desirable to specify the mapping of the problem onto qubits in the heavy-hex (or gross) lattice of IBM;reg; hardware from the outset if the structure of the problem lends itself to optimization earlier. It is also worth considering at this point what the outcome of the particular algorithm will be in preparation for the later execute step - for example, if the desired outcome involves inferring correlation functions using Hadamard tests, you might prepare to use Sampler, whereas specifying observables would use the Estimator and could provide many error mitigation options.

The output of this step is normally a collection of circuits or quantum operators that can be optimized for hardware in the next step.

## Optimize for target hardware
In this step you take the abstract circuits (or operators) produced from the map step and perform a series of optimizations on them. This can include mapping the route and layout of the circuit to physical qubit hardware, converting to basis gates of the hardware, and reducing the number of operations, all designed to optimize the likelihood of success in the later execute step. At this point you might also wish to test out your circuits with a simulator before executing on real hardware in the next step.

During this step, abstract circuits must be transpiled to Instruction Set Architecture (ISA) circuits. An ISA circuit is one that only consists of gates understood by the target hardware (basis gates), and any multi-qubit gates needed to obey any connectivity constraints (coupling map). Only ISA circuits can be run on IBM hardware using IBM Qiskit Runtime.
## Execute on target hardware
This step involves running your circuits on hardware and produces the outputs of the quantum computation. The ISA circuits produced in the previous step can be executed using either a Sampler or Estimator primitive from Qiskit Runtime, initialized locally on your computer or from a cluster or other heterogeneous compute environment. These can be executed in a Batch, which allows parallel transpilation for classical computational efficiency - or a Session, which allows iterative tasks to be implemented efficiently without queuing delays. During this step, there is also the option to configure certain error suppression and mitigation techniques provided by Qiskit Runtime.

Depending on whether you are using the Sampler or Estimator primitive, the outcome of this step will be different. If using the Sampler, the output will be per-shot measurements in the form of bitstrings. If using the Estimator, the output will be expectation values of observables corresponding to physical quantities or cost functions.

## Post-process results
This final step involves stitching the outputs from the prior step back together to obtain the desired result. This can involve a range of classical data-processing steps such as visualizing results, readout error mitigation techniques, marginalizing quasi-probability distributions to ascertain results on smaller sets of qubits, or post-selection on inherent properties of the problem, such as total spin, parity, or particle conservation by removing unphysical observables.

As the field moves from bespoke circuit construction to utility-scale workflows, the flexibility and ease with which Qiskit patterns allow users to compose the different steps of the pattern opens quantum computing to a wide variety of applications and techniques for easy use by quantum computational scientists.

# Guides demonstrating Qiskit patterns in action
## Guides focused on one or more pattern steps

- [Map problem to quantum circuits and operators](https://docs.quantum.ibm.com/guides/map-problem-to-circuits)
- [Optimize for target hardware](https://docs.quantum.ibm.com/guides/optimize-for-hardware)
- [Execute on target hardware](https://docs.quantum.ibm.com/guides/execute-on-hardware)
- [Post-process results](https://docs.quantum.ibm.com/guides/post-process-results)

## Guides focused on the full patterns workflow
- [Qiskit Serverless](https://docs.quantum.ibm.com/guides/serverless)

    - [Overview of Qiskit Serverless](https://docs.quantum.ibm.com/guides/serverless)
    - [Write your first Qiskit Serverless program](https://docs.quantum.ibm.com/guides/serverless-first-program)
    - [Run your first Qiskit Serverless workload remotely](https://docs.quantum.ibm.com/guides/serverless-run-first-workload)
    - [Manage Qiskit Serverless compute and data resources](https://docs.quantum.ibm.com/guides/serverless-manage-resources)
    - [Port code to Qiskit Serverless]()
- [Qiskit Functions](https://docs.quantum.ibm.com/guides/serverless-port-code)

    - [Q-CTRL Optimization Solver](https://docs.quantum.ibm.com/guides/q-ctrl-optimization-solver)
    - [QunaSys QURI Chemistry](https://docs.quantum.ibm.com/guides/qunasys-quri-chemistry)


# Quantum roadmap
- IBM's quantum roadmap provides a clear and structured path for the development of its quantum computing capabilities.
- The focus on scaling, error correction, middleware automation and global infrastructure expansion demonstrates IBM's commitment to making quantum technology commercially viable.
- IBM is positioning itself as a leader in quantum-centric supercomputing that is tied with goals to redefine the computational landscape and create new business value for clients.
The future of computing is quantum-centric.

IBM's quantum roadmap outlines the company's comprehensive strategy aimed at scaling quantum computing and expanding how they can be used for commercial and scientific applications. The roadmap extends beyond 2033 and breaks down into two main sections: the development and innovation roadmaps. These sections detail the company's efforts to develop modular quantum systems, integrate error correction, and enable quantum-centric supercomputing.

Based on information provided by IBM and at The Quantum Insider's Intelligence Platform, among other sources, here's a look into IBM's journey toward the realization of its vision of quantum-centric supercomputing, along with its strategies and its goals.

## From Scaling Qubits to Quantum-Centric Supercomputing
IBM's initial focus was on scaling the number of qubitsfundamental units of quantum information. The approach was straightforward: add qubits to increase computing power. However, in 2023, IBM shifted its strategy to focus on not just the quantity of qubits but the quality of gate operations. Gate operations, a measure of how efficiently a quantum system processes information, are becoming a key metric as IBM aims to enhance the workloads its quantum systems can handle.
### Quantum Utility and IBM Quantum System Two Milestones
In 2023, IBM claims it demonstrated "quantum utility," achieving a level where its quantum systems surpassed classical computers for specific tasks. This milestone marked an inflection point for the company, establishing that quantum computers are not just theoretical tools but practical, utility-scale machines. IBM's Qiskit SDK, the open-source quantum computing software development kit, and Qiskit Runtime, an optimized execution environment, have been instrumental in achieving this progress.

The introduction of the IBM Quantum System Two was a pivotal step on the company's quantum journey. As a modular architecture, System Two serves as the backbone for IBM's quantum-centric supercomputing model defined by IBM as connecting processors and optimizing classical and quantum communication to provide a way to take on larger-scale quantum computing tasks. The system integrates middleware for workload optimization, allowing automatic task distribution between quantum and classical resources, a crucial capability for quantum and classical parallel processing .

Expanding Global Quantum Infrastructure
IBM's strategy includes not just scaling technology but also infrastructure. In October 2024, the company inaugurated its first European quantum data center in Ehningen, Germany. This expansion allows IBM to provide utility-scale quantum computing services to European clients, marking an important step in its global quantum infrastructure.

The Ehningen center complements IBM's existing facilities in New York, which currently house a significant portion of the company's global quantum fleet. This regional expansion signifies IBM's effort to decentralize its quantum capabilities, reducing latency for users in different parts of the world and enhancing access to its computing power.

### The Evolution of IBM's Quantum Systems: Towards Error-Corrected Systems
Looking ahead, IBM's roadmap focuses on enhancing error correction one of the essential aspects of making quantum systems more reliable. Error correction helps extend and improve quantum coherence and computational reach, enabling the system to process more complex algorithms. IBM's development roadmap highlights that by 2025, the company plans to integrate error mitigation techniques within Qiskit Primitives, forming a robust foundation for developers to build quantum workflows.

The primitives are computational building blocks for larger applications with input units primitive unified blocs that need quantum resources to efficiently produce outputs. This update will allow algorithms to function with reduced noise, improving circuit quality and overall computation speed.

In the same timeframe, according to the roadmap, IBM aims to demonstrate a 1,000+ qubit system called "Flamingo". This system is designed as a modular assembly of processors, each containing multiple chips. The goal is to scale quantum systems significantly while maintaining performance and error rates. Such advancements are steps toward IBM's vision of a utility-scale quantum supercomputer, capable of processing large-scale problems across multiple domains such as security, chemistry, and optimization.

### Pushing Boundaries With Next-Gen Systems And Devices
Beyond 2025, IBM plans to launch the Starling system, a modular, error-corrected quantum supercomputer capable of running 100 million gates. This system represents IBM's ongoing efforts to refine error correction codes and incorporate dedicated classical hardware, ensuring computational efficiency and speed. The integration of classical and quantum nodes into a cohesive network aims to streamline resource management, enhancing the capability to tackle increasingly complex computations.

The longer-term outlook includes the Blue Jay system, a quantum supercomputer projected to incorporate 100,000 qubits by integrating thousands of logical qubits. IBM expects Blue Jay to achieve the capacity of running up to 1 billion gates, offering a scalable platform that could potentially unlock general applications in areas like security, machine learning, and materials discovery. Middleware improvements are also planned, focusing on noise-free quantum computations managed by distributed software tools working in tandem with classical resources.

### Middleware and Automation: Enabling Scalable Quantum Computing
A core component of IBM's quantum roadmap is the development of advanced middleware that automates and optimizes quantum workloads. Middleware is vital for distributing tasks across quantum and classical systems, ensuring efficient resource utilization. In 2025, IBM plans to introduce serverless tools, allowing users to focus on developing algorithms without managing the underlying infrastructure. Such tools are crucial for scaling quantum computing into everyday use, making the technology accessible for a broader range of applications.

The automation features in IBM's middleware include intelligent orchestration, which analyzes workflows to identify the optimal allocation of QPUs, communication channels, and classical resources. These advancements aim to extend the quantum system's reach, providing seamless operations even as the technology scales up.

Enhancing the Developer Experience With Qiskit And Code Assistants
As some of the pieces have already been mentioned, Qiskit is obviously an important part of the quantum roadmap. IBM released Qiskit in 2017 to serve as a first-of-its-kind research tool. According to IBM documentation, It offered an open-source, Python-based software development kit, library and framework to program quantum computers. Seven years, 100 releases, 550 open-source contributions, 550,000 users, and 3 trillion quantum circuits later, Qiskit 1.0 arrives as a mature Python package for running large-scale quantum experiments.

To foster a growing developer community and accelerate application development, IBM has integrated the Qiskit platform with Generative AI tools and AI-powered tools like Code Assistant. (Here's a recent breakdown on Qiskit Code Assistant on The Quantum Insider.) These tools are designed to streamline quantum programming, helping developers write code more efficiently and optimize circuits for specific hardware. As quantum systems become more complex, having accessible programming tools will be essential for expanding quantum computing's use cases beyond specialized research labs.

IBM's approach also includes the development of higher-level APIs and domain-specific libraries within Qiskit, aimed at abstracting the complexities of quantum circuits. By transitioning to a function-based paradigm, IBM seeks to make quantum technology more usable, ultimately opening up opportunities for industries ranging from pharmaceuticals to logistics.

Towards 2033 and Beyond: IBM's Quantum Ambitions
IBM's long-term quantum ambitions extend well into the next decade. The company aims to build systems capable of handling thousands of qubits, offering users a robust platform for tackling vast computational challenges. By leveraging scalable architectures and efficient error correction techniques, IBM envisions a future where quantum computers are an integral part of solving complex problems beyond the reach of classical systems.

The roadmap also emphasizes the integration of quantum systems with classical computing resources to create a truly heterogeneous computing environment. This fusion is seen as the key to unlocking the full potential of quantum-centric supercomputing, enabling breakthroughs in fields like cryptography, artificial intelligence, and large-scale optimization.

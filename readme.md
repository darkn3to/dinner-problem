<h1 align="center">Dinner Problem using Grover's Algorithm</h1>

This project employs Grover's Algorithm, a quantum computing approach, to tackle the boolean satisfiability (SAT) version of the Dinner Problem.

## Background

#### What is the Dinner Problem?

The Dinner Problem is a type of Boolean SAT problem where the goal is to determine an optimal arrangement of guests at a dinner based on specific criteria such as preferences, relationships, or interactions. This could involve deciding who should sit next to whom or ensuring that certain guests are not seated together to avoid conflicts or enhance the dining experience.

#### What is Boolean Satisfiability/B-SAT (SAT)

The Boolean satisfiability problem is about determining if a Boolean formula can be made TRUE by assigning truth values (TRUE or FALSE) to its variables. For example, the formula "a AND NOT b" is satisfiable because you can assign a = TRUE and b = FALSE to make the formula true. Conversely, "a AND NOT a" is unsatisfiable because no assignment of values to 'a' can make the formula true. SAT checks for such possibilities, making it a fundamental problem in computational logic and computer science.

#### Grover's Algorithm

Grover's Algorithm is a quantum algorithm that provides a quadratic speedup for searching unstructured databases compared to classical algorithms. It can find a specific item in a database in O(√N), where N is the total number of items, significantly reducing the search time needed. This makes it highly effective for problems where the solution involves searching through large datasets.

## Problem Statement

Dhruv is hosting a dinner party and he has invited five of his friends: Manas, Charlie, Ayaan, Abhinav, and Harsh. However, due to space constraints, he can only invite three friends to the dinner. 

Dhruv wants to ensure that the combination of friends he invites will result in a pleasant evening. He knows that:

1. Manas and Charlie have a lot in common and should be invited together.
2. Ayaan and Abhinav have recently had a disagreement, so they should not be invited together.
3. Harsh gets along with everyone.

Given these constraints, Dhruv wants to find all possible combinations of friends he can invite to ensure a pleasant evening. 

## Solution Approach

1. Create a five channel quantum circuit qᵢ. ```qᵢ = {q₀, q₁, q₂, q₃, q₄}```. Each qubit represents a friend's presence (q₀ represents Manas' presence, q₁ represents Charlie's presence and so on...).
2. Generate the combination of friends that satisfy the afore-mentioned conditions using ```generate_combinations()```.
3. Initialize the qubits in Superposition by applying Hadamard gate to each qubit. This allows the circuit to explore every possible state.
4. Create an oracle that identifies each valid state (each valid combination of friends). For each valid state, the oracle constructs a unique diagonal matrix that, when applied, imparts a negative phase specifically to that state, effectively marking it.
5. Apply the oracle to the superposition of states. This marks the valid combinations by flipping their phase.
6. Apply the diffuser (also known as the amplitude amplification step). This step consists of applying Hadamard and X gates to all qubits, applying a phase shift to the |00000⟩ state, and then applying X and Hadamard gates again. This process inverts the amplitudes of all states about the average amplitude, which has the effect of amplifying the amplitudes of the marked states and decreasing the amplitudes of the unmarked states.
7. Measure the qubits. The result will be a string of bits that represents one of the valid combinations of friends. The probability of obtaining a particular valid combination is proportional to the square of its amplitude, so the marked states (the valid combinations) are more likely to be measured than the unmarked states.

## Oracle & Diffuser Explained
#### Oracle

The diagonal matrix is multiplied with the state vector of the state to obtain a marked state with negative phase.
Suppose we want to find a state ∣10⟩ in a two qubit system. The diagonal matrix for the state can be represented as:
```
[1  0  0  0]
[0  1  0  0]
[0  0 -1  0]
[0  0  0  1]
```
and the state vector for the state ∣10⟩ would be:
```
[0]
[0]
[1]
[0]
```
Now the oracle would mark the state by doing so:
```
[1  0  0  0]       [0]         [ 0]
[0  1  0  0]   *   [0]    =    [ 0]
[0  0 -1  0]       [1]         [-1]
[0  0  0  1]       [0]         [ 0]
```
Thus, the state ∣10⟩ has been marked. PS: This was just a demo of how to the oracle functions. The actual diagonal matrix would be of the size: ```2⁵ * 2⁵ = 32 * 32``` which would have been quite large to represent here. Similarly, the state vector would be of the size: ```2⁵ * 1```. 

You may uncomment the code from the oracle implementation to see by yourself.

#### Diffuser
The diffuser is a crucial part of Grover's algorithm. It's responsible for amplifying the probability amplitudes of the marked states, thereby increasing the likelihood of these states being measured.

The diffuser operates by performing an inversion about the average amplitude. Here's how it works:

1. Apply a Hadamard gate to all qubits. This puts the qubits into superposition, allowing the algorithm to explore all possible states.

2. Apply an X (NOT) gate to all qubits. This flips the state of each qubit.

3. Apply a phase shift to the |00000⟩ state. This is done by creating a diagonal matrix from the state vector of the |11111⟩ state and appending it to the circuit. The diagonal matrix has -1 at the position corresponding to the |00000⟩ state and 1 elsewhere. This effectively flips the amplitude of the |00000⟩ state.

4. Apply an X (NOT) gate to all qubits again. This undoes the flipping of the states from step 2.

5. Apply a Hadamard gate to all qubits again. This undoes the superposition from step 1, but with the amplitudes of the marked states now amplified and the amplitudes of the unmarked states decreased.

The diffuser is represented as a `QuantumCircuit` object and is visualized using the `draw()` method.

## Requirements/Dependencies

- Qiskit: Qiskit is an open-source quantum computing software development framework provided by IBM. It allows users to write, simulate, and run quantum algorithms on real quantum machines and simulators accessible through IBM's cloud platform.

- Matplotlib: Matplotlib is an open-source plotting library for the Python programming language which provides a wide range of tools for creating static, interactive, and animated visualizations in Python, making it one of the most popular libraries for data visualization tasks.

- Jupyter Notebook: Jupyter Notebook is an open-source web application that allows you to create and share documents that contain live code, equations, visualizations, and narrative text. 

## Usage

- Clone the repository by using the command:
  
   ```cmd
   git clone https://github.com/darkn3to/dinner-problem.git
   ```
   
   or simply download the zip file from the code dropdown button above.

- Install the dependencies by using `pip install dependency_name`.

- Run `grover.ipynb`.

## Results Analysis

Upon successful execution of the code, two key outputs are generated: a circuit diagram and a histogram of probabilities for each state.

1. **Circuit Diagram**: The circuit diagram provides a visual representation of the quantum operations performed on the qubits. It starts with the initialization of the qubits, followed by the application of the oracle and the amplitude amplification operations. The final operation is the measurement of each qubit. This diagram is useful for understanding the sequence of operations and for debugging the quantum circuit.

![Final Circuit Diagram](https://github.com/darkn3to/dinner-problem/assets/62509177/012f556e-816d-4315-908d-3b58770521fe)

2. **Histogram**: The histogram displays the probabilities of each state after the quantum operations. The states are represented on the x-axis, and the corresponding probabilities are represented on the y-axis. The states that are possible solutions to the problem are highlighted in a different color. This visualization is useful for understanding the effect of the quantum operations on the state of the system. In an ideal scenario, the marked states (the solutions) should have significantly higher probabilities than the unmarked states. If this is not the case, it may indicate that the oracle or the amplitude amplification operation is not working as expected.

![Histogram](https://github.com/darkn3to/dinner-problem/assets/62509177/fc20e9cc-04c5-46de-a527-7bd58c2efbff)

The execution of our quantum algorithm has led to three states being marked as potential solutions: `11001`, `11011`, and `11101`. These binary states correspond to the combinations of friends who can be invited to the party without breaking any of the given conditions.

Here's how to interpret these states:

- `11001` corresponds to Manas, Charlie, and Harsh.
- `11011` corresponds to Manas, Charlie, Abhinav, and Harsh.
- `11101` corresponds to Manas, Charlie, Ayaan, and Harsh.

These states are highlighted in the histogram of probabilities, indicating that they have a higher probability of being measured as a result of the quantum operations performed by our algorithm. This means that these combinations of friends are the most likely solutions to our problem, according to the rules we've defined.

By using quantum computation and specifically Grover's algorithm, we've been able to efficiently search for and identify these optimal solutions.

## Resources

- [Refer this article for getting up to speed on Quantum Computing basics](https://blog.innostation.org/understanding-quantum-computing-mathematically-f42f9589e78b)
- [Dinner Problem using Qiskit](https://www.youtube.com/watch?v=ePr2MgQkqL0)
  




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

1. Create a five channel quantum circuit qᵢ. ```qᵢ = {q₀, q₁, q₂, q₃, q₄}```. Each qubit represents a friend's name in lexicographic order (q₀ represents Abhinav's presence, q₁ represnts Ayaan's presence and so on...). 
3. Generate the combination of friends that satisfy the afore-mentioned conditions using ```generate_combinations()```.
4. Initialize the qubits in Superposition by applying Hadamard gate to each qubit. This allows the circuit to explore every possible state.
5. Create an oracle that identifies each valid state (each valid combination of friends). For each valid state, the oracle constructs a unique diagonal matrix that, imparts a negative phase specifically to that state, effectively marking it. The diagonal matrix is multiplied with the state vector of the state to obtain a marked state with negative phase.

Suppose we want to find a state 01 in a two qubit system. 

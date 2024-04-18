<h1 align="center">Dinner Problem using Grover's Algorithm</h1>

This project employs Grover's Algorithm, a quantum computing approach, to tackle the boolean satisfiability (SAT) version of the Dinner Problem, a unique and intriguing challenge.

###What is the Dinner Problem?

The Dinner Problem is a type of Boolean SAT problem where the goal is to determine an optimal arrangement of guests at a dinner based on specific criteria such as preferences, relationships, or interactions. This could involve deciding who should sit next to whom or ensuring that certain guests are not seated together to avoid conflicts or enhance the dining experience.

###What is Boolean Satisfiability/B-SAT (SAT)

The Boolean satisfiability problem is about determining if a Boolean formula can be made TRUE by assigning truth values (TRUE or FALSE) to its variables. For example, the formula "a AND NOT b" is satisfiable because you can assign a = TRUE and b = FALSE to make the formula true. Conversely, "a AND NOT a" is unsatisfiable because no assignment of values to 'a' can make the formula true. SAT checks for such possibilities, making it a fundamental problem in computational logic and computer science.

Dhruv is hosting a dinner party and he has invited five of his friends: Manas, Charlie, Ayaan, Abhinav, and Harsh. However, due to space constraints, he can only invite three friends to the dinner. 

Dhruv wants to ensure that the combination of friends he invites will result in a pleasant evening. He knows that:

1. Manas and Charlie have a lot in common and should be invited together.
2. Ayaan and Abhinav have recently had a disagreement, so they should not be invited together.
3. Harsh gets along with everyone.

Given these constraints, Dhruv wants to find all possible combinations of three friends he can invite to ensure a pleasant evening. 

Use Grover's search algorithm to find all valid combinations of three friends that Dhruv can invite to the dinner. Represent each friend by a qubit in a 5-qubit quantum system, where the state of the qubit indicates whether that friend is invited (1) or not invited (0). 

The oracle should mark the valid combinations of friends, and the Grover's algorithm should be used to amplify these marked states. Run the algorithm and measure the final state of the qubits to find the valid combinations.

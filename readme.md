**Problem Statement:**

Dhruv is hosting a dinner party and he has invited five of his friends: Manas, Charlie, Ayaan, Abhinav, and Harsh. However, due to space constraints, he can only invite three friends to the dinner. 

Dhruv wants to ensure that the combination of friends he invites will result in a pleasant evening. He knows that:

1. Manas and Charlie have a lot in common and should be invited together.
2. Ayaan and Abhinav have recently had a disagreement, so they should not be invited together.
3. Harsh gets along with everyone.

Given these constraints, Dhruv wants to find all possible combinations of three friends he can invite to ensure a pleasant evening. 

Use Grover's search algorithm to find all valid combinations of three friends that Dhruv can invite to the dinner. Represent each friend by a qubit in a 5-qubit quantum system, where the state of the qubit indicates whether that friend is invited (1) or not invited (0). 

The oracle should mark the valid combinations of friends, and the Grover's algorithm should be used to amplify these marked states. Run the algorithm and measure the final state of the qubits to find the valid combinations.
# Quantum Trust

Quantum Trust is a two-player strategy game combining classical game theory with quantum mechanics. Players compete by choosing how much to trust one another, with their decisions encoded into quantum circuits that determine the outcome of each round.

The project was collaboratively developed using Python and Qiskit.

## Gameplay

Each player begins with 3 points and selects a trust percentage between 0% and 100% each round. These values represent each player's willingness to cooperate or betray their opponent.

The game continues until one of the following conditions is met:

- A player reaches 9 points, winning a prize of $1,000,000.
- A player's score drops to zero or below, resulting in a loss.
- Both players reach 9 points simultaneously, earning $100 each.
- Both players reach zero or below simultaneously, resulting in both players losing their assets.

## Quantum Circuit Implementation

Each round constructs a two-qubit quantum circuit using Qiskit. Players' trust percentages (`t`) are encoded into qubit rotations, and quantum operations determine the resulting measurement probabilities.

The circuit follows this sequence:

1. **Superposition:** Hadamard gates are applied to both qubits, placing them into superposition.
2. **Decision Encoding:** Each player's trust percentage is converted into a rotation angle:

   $$\theta = \pi\left(1-\frac{t}{100}\right)$$

   This angle determines the $R_y(\theta)$ rotation applied to each player's qubit. Higher trust values produce smaller rotations, while lower trust values produce larger rotations.
3. **Entanglement:** A controlled-X (CX) gate entangles the two qubits, linking the players' quantum states.
4. **Interference:** A second layer of Hadamard gates introduces quantum interference.
5. **Measurement:** Both qubits are measured in the computational basis, producing one of four possible outcomes: `00`, `01`, `10`, or `11`.

These operations allow players' decisions to interact through superposition, entanglement, and quantum interference.

## Measurement and Scoring

Each quantum circuit is simulated using **1,024 shots**. The resulting measurement counts represent the frequency of each possible two-qubit outcome.

Rather than calculating scores from the entire probability distribution, the game selects the **most frequently measured outcome** to determine the round's result.

A predefined payoff dictionary maps the selected measurement outcome to the corresponding changes in each player's score. Scores are updated accordingly, and the game proceeds to the next round.

<img width="4032" height="1035" alt="image" src="https://github.com/user-attachments/assets/4ae9677f-3fdd-48c6-a1dc-ed97b52eb037" />

This approach retains quantum measurement statistics while using the dominant outcome to produce a straightforward competitive game.

## Project Goals

Quantum Trust explores how quantum computing concepts can be incorporated into interactive game mechanics.

By encoding strategic decisions into quantum states, the game demonstrates how superposition, entanglement, interference, and measurement can influence competitive outcomes. Players can experiment with different trust levels and observe how changes in their decisions affect the resulting measurement statistics.

## Technologies

- Python
- Qiskit
- Quantum circuit simulation

## Running the Project

The game is implemented in a Jupyter Notebook.

1. Clone or download this repository.
2. Open `Quantum_Trust.ipynb` using Jupyter Notebook, JupyterLab, or Google Colab.
3. Install the required dependencies if they are not already installed:

   ```bash
   pip install qiskit --quiet
   pip install qiskit-aer --quiet
   ```

4. Run the notebook cells sequentially to initialize and play the game.

Alternatively, open the notebook directly through GitHub to explore the source code.

## Contributors

Collaboratively developed by Christian Naviengkham and SriJishnu Devarapalli.

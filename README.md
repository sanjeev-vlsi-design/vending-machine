Vending Machine FSM Design
Overview
This is a finite state machine (FSM) implementation of a vending machine in Verilog. The vending machine accepts coins, dispenses products, and returns change.

Inputs
clk: Clock signal driving state transitions.
rst: Reset signal initializing the machine to its default state (Idle).
coin [3:0]: Coin input; accepts values of 5 or 10.
select [1:0]: Product selection signal:
00 → Product A
01 → Product B
10 → Product C
11 → Product D
Outputs
deliver_A, deliver_B, deliver_C, deliver_D: Signals to dispense the selected product. Only one will be active.
change [3:0]: Returns change when the inserted amount exceeds the product price.
Product Prices
Product A: 15
Product B: 20
Product C: 25
Product D: 30
States
Idle: Waiting for coin input.
Collect: Collecting coins and checking balance against the selected product price.
Product: Dispensing the product, calculating, and returning change.
Behavior
1. Idle State
Waits for coin input (5 or 10 units).
Transitions to Collect state after accepting a valid coin.
2. Collect State
Accumulates the balance with additional coins.
Checks if the balance is sufficient for the selected product:
If yes, transitions to the Product state.
Otherwise, remains in Collect state.
3. Product State
Dispenses the selected product by activating the corresponding deliver_X signal.
Calculates and outputs change (balance - product price).
Resets balance to 0 and transitions back to the Idle state.
Example Scenario
Insert Coins:
Start in Idle.
Insert 10 → Transition to Collect, balance = 10.
Insert 10 → balance = 20.
Select Product:
Select Product B (Price_B = 20).
Balance matches the price, transition to Product.
Dispense Product:
Dispense Product B (deliver_B = 1).
Return no change (change = 0).
Reset balance = 0, transition back to Idle.
State Diagram
Idle → Collect (on coin input).
Collect → Product (when balance is sufficient for the selected product).
Product → Idle (after dispensing the product and returning change).

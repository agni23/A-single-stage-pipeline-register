A-single-stage-pipeline-register

1. Handshake Protocol
Input interface: in_valid && in_ready triggers data capture
Output interface: out_valid && out_ready triggers data release
Backward pressure propagates: in_ready = ~reg_valid | (reg_valid & out_ready)

2. State Behaviour
Empty state (reg_valid == 0): This will accept new data immediately
Full state (reg_valid == 1): This will only accept new data when downstream is ready (out_ready == 1)

3. Critical Cases Handled
Full register, downstream not ready: in_ready = 0, input stalls
Pass-through scenario: When full and out_ready && in_valid, register updates with new data in same cycle
Reset behavior: Clears valid bit, optionally clears data

4. Synthesis Considerations
Uses always_ff for sequential logic and always_comb for combinational logic
Clear reset (synchronous active-low)
No latches inferred (all branches of always_ff covered)
Parameterized width for reusability

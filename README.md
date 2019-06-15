# PROBLEM:
Unity.Mathematics' types agressively implicitly cast. Using these as method arguments leads to unproductive complexity.

# SOLUTION:
Create intermediary types that implicitly cast ONLY to/from very strict equivalents. Use them as method arguments only.

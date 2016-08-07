**Collecting memory dumps**

- If the suspicious mem increase happens when running multiple iterations, run one or few iterations.
- If the test is not executing multiple iterations, just bring the system to an initial state.
- if operation is supported, trigger a Garbage collect 
- Take a look at Memory (Private working set) and note down the value
- Take a mem dump
- Run one or more iterations
- Trigger again Garbage collect
- Take a look at Memory (Private working set) and note down the value. 
- If the amount is almost the same, no significant mem leak was detected. You could continue running iterations.
- If the amount of memory is much larger, there is a suspicion of leaks. Take a mem dump.

**Narrowing down the cause - managed or unmanaged**

Perfmon is one of the tools which could be used for pointing to the type problem.
- Those 2 counters need to be analyzed:
"Process/Private bytes"
".Net CLR mem/Bytes in all heaps"
- If the private bytes is increasing but the bytes in all heaps remain constant, the problem is located in native code.
- If both are increasing then it's a managed memory consumption.

**Debug unmanaged leak**

1. Install Debug Diag
2. instrument executable, save dump
3. Load dump file and start analysis
 
**Using .Net Memory Profiler for memory related investigation**

- Load mem dump or attach to process (preferable)
- Check overview tab
- If specific object type is tracked, set the filter in the first row of the grid
- Check the total amount of heap on the grid footer
- Sort objects by Live Bytes, Total
- Click largest consumer, a list of instances is displayed
- Click shortest root paths for grouping the instances so root can be inspected
- Check the reference tree to see if objects are leaking or are long lived unnecessarily.
- Check native memory tab to view the breakdown of the heap and gaps (the gaps cannot be reclaimed even if the leak is solved)

Jaynish Patel

In order to evaluate the lottery scheduler, I added a benchmarching system called lotterybench which uses 5 child processes which have a set ticket count. {100, 50, 10, 5, 1} tickets.

All are executed in the same CPU workload ensuring identical testing for different ticket counts based on the finish time (ticks) and the cpu time (runtime).

Results:
Patterns across the counts observed show that 100 ticket count process finished first, the 50 count is observed as second, 10th, 5 and 1 are followed after which confirms that the CPU time is proportional to the set ticket counts.

The runtime of the CPU was airly similar in most of the processes running roughyly 100-110 ticks per which shows that the proceses executed have roughly the same workload and the difference in the finish time was due to scheduling not the workload size.

Smaller scale Benchmark runs
Lottery Scheduler Benchmark (Default)

PID 5  Tickets  100  Finished after 0 ticks
PID 6  Tickets  50  Finished after 0 ticks
PID 8  Tickets  5  Finished after 0 ticks
PID 7  Tickets  10  Finished after 0 ticks
PID 9  Tickets  1  Finished after 0 ticks
Total Duration = 434 ticks

Benchmark 2000
PID 11  Tickets  100  Finished after 0 ticks
PID 14  Tickets  5  Finished after 0 ticks
PID 12  Tickets  50  Finished after 0 ticks
PID 13  Tickets  10  Finished after 0 ticks
PID 15  Tickets  1  Finished after 0 ticks
Total Duration = 192 ticks


Larger scale Benchmark Runs
Benchmark 5000000000
PID 17  Tickets  100  Finished after 1426 ticks
PID 18  Tickets  50  Finished after 1598 ticks
PID 19  Tickets  10  Finished after 2532 ticks
PID 20  Tickets  5  Finished after 2757 ticks
PID 21  Tickets  1  Finished after 3464 ticks
Total Duration = 3695 ticks


The variation etween the minimum and maximum is expected because if a lower ticket process is to happen then it wins the early lottery and vice versa for larger ticket processes.

Relative Share over Long Runs showsthat the overly sufficiednt long workloads persist, then the scheduler will align with the expected lottery scheduling based on CPU = tickets / total tickets.
Higher ticket process will receive more scheduling allowing it to complete sooner. 

Notes on variance predict that lottery scheduling is probabilistic meaning that the short runs show ordering variations, the lower ticket process may win early loteries and the total runtime (cpu) varies based on run to run.

This validates all that the lottery scheduler is correctly implemented allocating the CPU time based on the ticket counts while still maintaining its probabilistic traits.
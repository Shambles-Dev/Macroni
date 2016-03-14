Availability
============

Reservation/quota describes a non-negative integer that serves both purposes.  It determines the minimum and maximum amount of a resource available to a component.

<table>
  <tr>
    <th colspan="2">Sandboxes</th>
  </tr>
  <tr>
    <th>Problem</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td><p>Sandbox space consumption might have been a problem.</p></td>
    <td><p>Macroni’s kernel or runtime system uses delegable sandbox space reservations/quotas to prevent this problem.  Macroni’s event system uses those sandbox space reservations/quotas to implement <a href="https://awesome-architecture.com/back-pressure/">back pressure</a> to maintain this solution.</p></td>
  </tr>
  <tr>
    <td><p>Sandbox space exclusion might have been a problem.</p></td>
    <td><p>Macroni’s kernel or runtime system uses <a href="https://aws.amazon.com/builders-library/using-load-shedding-to-avoid-overload/">load shedding</a> of processes that are not intended to keep executing in the background to recover from this problem.  It uses transparent persistence to prevent data loss in this situation.</p></td>
  </tr>
  <tr>
    <td><p>Sandbox space fragmentation might have been a problem.</p></td>
    <td>
      <p>Macroni’s kernel or runtime system uses delegable sandbox count reservations/quotas and <a href="https://www.tutorialspoint.com/operating_system/os_memory_allocation_qa2.htm">best-fit allocation</a> to limit this problem and load shedding of processes that are not intended to keep executing in the background to recover from it between sandboxes.  It uses transparent persistence to prevent data loss in this situation.</p>
      <p>Macroni’s runtime system uses <a href="https://en.wikipedia.org/wiki/Tracing_garbage_collection#Moving_vs._non-moving">compacting</a> garbage collection to recover from this problem within sandboxes.</p>
    </td>
  </tr>
</table>

<table>
  <tr>
    <th colspan="2">Scheduler</th>
  </tr>
  <tr>
    <th>Problem</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td><p>Schedule time consumption might have been a problem.</p></td>
    <td><p>Macroni’s kernel or runtime system uses microrebooting to recover from this problem when a process’ main sandbox crashes or one of its event handlers times out.</p></td>
  </tr>
  <tr>
    <td><p>Schedule time exclusion might have been a problem.</p></td>
    <td>
      <p>Macroni’s scheduler is <a href="https://en.wikipedia.org/wiki/Preemption_(computing)">preemptive</a> to prevent sandboxes from refusing to relinquish cores.</p>
      <p>Macroni’s scheduler uses <a href="https://en.wikipedia.org/wiki/Scheduling_(computing)#Priority_scheduling">prioritization</a> to limit <a href="https://en.wikipedia.org/wiki/Latency_(engineering)">latency</a>.  Macroni’s event system uses a solution similar to (optional) <a href="https://en.wikipedia.org/wiki/Priority_inheritance">priority inheritance</a> to prevent a problem similar to <a href="https://en.wikipedia.org/wiki/Priority_inversion">priority inversion</a>.</p>
      <p>Macroni’s scheduler is <a href="https://en.wikipedia.org/wiki/Fair_queuing">fair</a> (prioritized <a href="https://en.wikipedia.org/wiki/Round-robin_scheduling">round-robin</a>) to prevent sandboxes from <a href="https://en.wikipedia.org/wiki/Starvation_(computer_science)">starving</a>.  It uses <a href="https://en.wikipedia.org/wiki/Aging_(scheduling)">aging</a> to prevent starvation despite prioritization.</p>
      <p>Macroni’s event system is <a href="https://en.wikipedia.org/wiki/Message_passing#Asynchronous_message_passing">asynchronous</a> to prevent sandboxes from <a href="https://en.wikipedia.org/wiki/Blocking_(computing)">blocking</a> others.</p>
    </td>
  </tr>
  <tr>
    <td><p>Schedule time fragmentation might have been a problem.</p></td>
    <td><p>Macroni’s kernel or runtime system uses delegable sandbox count reservations/quotas to limit this problem and load shedding of processes that are not intended to keep executing in the background to recover from it.  It uses transparent persistence to prevent data loss in this situation.</p></td>
  </tr>
</table>

<table>
  <tr>
    <th colspan="2">I/O</th>
  </tr>
  <tr>
    <th>Problem</th>
    <th>Solution</th>
  </tr>
  <tr>
    <td><p>I/O space consumption might have been a problem.</p></td>
    <td><p>Macroni’s file system uses per-program space reservations/quotas to prevent this problem.</p></td>
  </tr>
  <tr>
    <td><p>I/O space fragmentation might have been a problem.</p></td>
    <td><p>Macroni’s file system uses tail packing to limit this problem and defragmentation to recover from it.</p></td>
  </tr>
  <tr>
    <td><p>I/O time consumption can be a problem.</p></td>
    <td><p><a href="https://en.wikipedia.org/wiki/Timeout_(computing)">Timeouts</a>, <a href="https://en.wikipedia.org/wiki/Automatic_repeat_request">retries</a>, and <a href="https://en.wikipedia.org/wiki/Failover">failovers</a> can be used to recover from this problem (e.g. timeout unresponsive network connections).</p></td>
  </tr>
  <tr>
    <td><p>I/O time exclusion can be a problem.</p></td>
    <td><p>The user can be informed of the cause of this problem and can decide how to recover from it (e.g. terminate the process that is locking a file).</p></td>
  </tr>
  <tr>
    <td><p>I/O time fragmentation can be a problem.</p></td>
    <td><p>Load shedding can be used to recover from this problem (e.g. load shed excessive network connections).</p></td>
  </tr>
</table>


## See Also
* [Events](Events.md)
* [File System](File_System.md)
* [Garbage Collector](Garbage_Collector.md)
* [I/O](Input_Output.md)
* [Microrebooting](Microrebooting.md)
* [Packages](Packages.md)
* [Sandboxes](Sandboxes.md)
* [Scheduler](Scheduler.md)
* [Transparent Persistence](Transparent_Persistence.md)
* [User Interface](User_Interface.md)

<script>
// Javascript program to implement
// Shortest Remaining Time First
// Shortest Remaining Time First (SRTF)

class Process
{
	constructor(pid,bt,art)
	{
		this.pid = pid; // Process ID
		this.bt = bt; // Burst Time
		this.art = art; // Arrival Time
	}
}

// Method to find the waiting time for all
	// processes
function findWaitingTime( proc,n,wt)
{
	let rt = new Array(n);
		
		// Copy the burst time into rt[]
		for (let i = 0; i < n; i++)
			rt[i] = proc[i].bt;
		
		let complete = 0, t = 0, minm = Number.MAX_VALUE;
		let shortest = 0, finish_time;
		let check = false;
		
		// Process until all processes gets
		// completed
		while (complete != n) {
		
			// Find process with minimum
			// remaining time among the
			// processes that arrives till the
			// current time`
			for (let j = 0; j < n; j++)
			{
				if ((proc[j].art <= t) &&
				(rt[j] < minm) && rt[j] > 0) {
					minm = rt[j];
					shortest = j;
					check = true;
				}
			}
		
			if (check == false) {
				t++;
				continue;
			}
		
			// Reduce remaining time by one
			rt[shortest]--;
		
			// Update minimum
			minm = rt[shortest];
			if (minm == 0)
				minm = Number.MAX_VALUE;
		
			// If a process gets completely
			// executed
			if (rt[shortest] == 0) {
		
				// Increment complete
				complete++;
				check = false;
		
				// Find finish time of current
				// process
				finish_time = t + 1;
		
				// Calculate waiting time
				wt[shortest] = finish_time -
							proc[shortest].bt -
							proc[shortest].art;
		
				if (wt[shortest] < 0)
					wt[shortest] = 0;
			}
			// Increment time
			t++;
		}
}

// Method to calculate turn around time
function findTurnAroundTime(proc,n,wt,tat)
{
	// calculating turnaround time by adding
		// bt[i] + wt[i]
		for (let i = 0; i < n; i++)
			tat[i] = proc[i].bt + wt[i];
}

// Method to calculate average time
function findavgTime(proc,n)
{
	let wt = new Array(n), tat = new Array(n);
		let total_wt = 0, total_tat = 0;
		
		// Function to find waiting time of all
		// processes
		findWaitingTime(proc, n, wt);
		
		// Function to find turn around time for
		// all processes
		findTurnAroundTime(proc, n, wt, tat);
		
		// Display processes along with all
		// details
		document.write("Processes " +
						" Burst time " +
						" Waiting time " +
						" Turn around time<br>");
		
		// Calculate total waiting time and
		// total turnaround time
		for (let i = 0; i < n; i++) {
			total_wt = total_wt + wt[i];
			total_tat = total_tat + tat[i];
			document.write(" " + proc[i].pid +
			"      "
			+ proc[i].bt + "    " + wt[i]
			+ "    " + tat[i]+"<br>");
		}
		
		document.write("Average waiting time = " +
						total_wt / n+"<br>");
		document.write("Average turn around time = " +
						total_tat / n+"<br>");
}

// Driver Method
let proc=[new Process(1, 6, 1),
							new Process(2, 8, 1),
							new Process(3, 7, 2),
							new Process(4, 3, 3)];
findavgTime(proc, proc.length);


// This code is contributed by rag2127

</script>

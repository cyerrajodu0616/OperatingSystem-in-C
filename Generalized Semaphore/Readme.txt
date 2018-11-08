a.	How many threads/processes are there?
1.	There are two threads in my project.
1.	Producer Thread
2.	Consumer Thread
b.	What does each thread simulate?
1.	Producer Thread
1.	This thread will check if there are any resource is available to use. If resource is available then this thread will generate a random number and increment the empty semaphore and decrement full semaphore. If resource is not available then thread will wait for availability of empty resource.
2.	Consumer Thread
1.	This thread will check if there is any resource have data by checking in full semaphore, If there is data in full semaphore then it will apply Mutual exclusive lock on that resource and read that data then release lock and increment empty semaphore. 
c.	Will each thread be blocked at some time of simulation? If yes, explain the circumstances.
1.	Yes
The Producer thread is blocked when the buffer is full and the Consumer thread is blocked when the buffer is empty.
Example:
	If Number of slots available in buffer =2
	Number of items to produce = 10

If there is no data in Global variable to consume then the consumer thread will be blocked till producer thread produces any data.
		Once the producer thread produces 2 data points then there will no available resource for Producer thread to utilize so until consumer thread consumes the produced value Producer thread will be blocked from utilizing resources further.
d.	When will a blocked thread be waked up, and by whom?
1.	Producer thread will be waked up by Empty_Semaphore (sem_post(&empty_semaphore) )when the consumer thread consumes data from global resource ( empty semaphore > 0 ).
2.	Consumer thread will be waked up by Full_semaphore (    sem_post(&full_semaphore) ) when the producer thread produces data into global resource ( Full Semaphore >  0 ).
e.	How many mutex locks/semaphores are there in your code, what is the purpose for having each?
1.	My code have 1 Mutex lock
1.	This will apply mutal exclusive lock on Critical section, So that this will helpful for thread synchronization.
2.	2 Semaphore (Empty and Full semaphore)
1.	Empty Semaphore will give number of threads can access the resource simultaneously. If empty semaphore is initialized with 3 then 3 threads can access critical section simultaneously. Each thread will decrement empty semaphore by 1 after entering into critical section so if empty semaphore is 0 then no other threads can access critical section. This thread have to wait until the thread in critical section leaves. Producer thread generates data and decrement empty semaphore by 1 and increment full semaphore by 1.
2.	Full Semaphore: This will be initialized to 0. Whenever there is data to consume then this semaphore is incremented by 1. If Full semaphore value is greater than 0 then the consumer thread will read that data and decrement the full semaphore by 1.
f.	How does your program terminate?
1.	User have to give number items to produce.
2.	Once Producer thread produces these many items then Producer thread will terminate.
3.	Once Consumer thread also consumes all the items produced by producer thread then Reducer thread will terminate 
4.	Once Producer and Reducer threads are terminated then the program will terminate. 

# Simulate_CPU_Schedule

#Setup

Consider a single person arcade game machine located in a shopping centre. While many customers wish to play, there is only one machine, so it is a shared resource. Customers willing to play arrive at random times and if the machine is occupied, they need to wait. This is a very advanced shopping centre and the use of the machine is facilitated by a robot manager (programmed by you!). In particular, the robot may decide that a customer is playing for too long and ask the customer to release the machine and move back to the waiting queue.

Based on the membership with the gaming company, there are two customer priorities: high for members and regular for non-members. Also, to facilitate scheduling, each customer must declare how many time units they will be playing for in total. Once a customer spends this amount of time at the machine (in one or multiple sessions), they leave.

I have write a program that decides which customer should be playing when.

#Data Format

An input data file is a simulated list of arriving customers. Input data files will be named "data_*.txt", where asterisk will be replaced by a random number (not relevant for you). Each row in such a file describes customer ID, priority (0 for high, 1 for regular), arrival time, and the desired amount of play time. 

Example:

c00 0 6 23
c01 1 20 13
c02 1 28 17
c03 1 38 28
...
In the first line, customer c00 arrived at time 6. This customer is a member and has a high priority. This customer wishes to play for 23 units of time in total. Note that 0 denotes high priority, while 1 denotes regular priority.

An output data file is a log of machine usage as a result of a particular scheduling approach. For a given input file, an output file can be generated either using a program in "baseline.cpp" (provided) or your program in "scheduler.cpp" (your submission). Each such output file is also called a scheduling.

Each row of the output file describes who was occupying the machine at a particular time slot (starting from 0). If the machine was not occupied, the row will list -1, otherwise it will show customer ID (without letter "c").

Example:

0 -1
1 -1
2 -1
3 -1
4 -1
5 -1
6 0
7 0
...
In this example, the machine was unoccupied in time slots 0, ..., 5. Then starting from time slot 6, the machine was used by customer 0.

#Valid Scheduling

If a customer arrives at time X, it can start occupying the machine starting from time slot X, but not earlier
If a customer wishes to play for N time slots, the total number of time slots occupied by that customer in the output must be N
Play time demand must be satisfied as above for every customer in the input file
There not need to be a gap between customers, two consecutive time slots can be occupied by two different customers
The output file must not contain customers that were not present in the input
The output file must list all time frames sequentially, starting from 0. There should be no time gaps. The output must cover enough time frames to satisfy demand of all customers
The last time slot in your scheduling should be after all customers are satisfied, and it should denote an empty machine (-1 as customer ID)
If the above conditions are satisfied, the scheduling is considering valid. However, some valid scheduling are better than others (see below)

#Definitions

total wait time = sum of wait times for all customers in the given input file
in some cases above, the total wait time includes only high priority or only regular priority customers
wait time for a customer = number of time slots such that (i) the customer has arrived at or before that time slot (ii) customer's play time demand has not been satisfied by this time, and (iii) the customer is not scheduled on the machine at this slot
longest response time = maximum response time across customers in the given input
response time for a customer = index of the time slot where the customers plays for the first time minus index of time slot where the customer arrived
example: customer 0 arrived at time 5, but the first time they have a chance to play is time slot 10. Response time for this customer is 10 - 5 = 5
number of switches = number of time slots (starting from 1), such that the occupation in the previous time slot doesn't match the occupation in this time slot
example: there are 3 switches in this schedule
0 -1
1 -1
2 0
3 0
4 1
5 -1

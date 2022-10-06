This is a self-running simulator that imitates a restaurant queue and tables' arrangement. Self-running means that once started it runs till 1000 iterations are reached or till stack overflow happens (if you don't stop it before, of course). You don't need to provide it any data. In my opinion, about 100 iterations is enough to see how it works.
The program is a solution to the following challenge:

       "Your restaurant has a set of tables of different sizes: each table can accommodate 2, 3, 4, 5 or 6 persons.
        Clients arrive alone or in groups, up to 6 persons. Clients within a given group must be seated together
        at one table, hence you can direct a group only to a table, which can accommodate them all. If there is
        no table with the required number of empty chairs, the group has to wait in the queue.

        Once seated, the group cannot change the table, i.e. you cannot move a group from one table to another
        to make room for new clients.

        Client groups must be served in the order of arrival with one exception: if there is enough room at a table
        for a smaller group arriving later, you can seat them before the larger group(s) in the queue. For example,
        if there is a six-person group waiting for a six-seat table and there is a two-person group queuing or
        arriving you can send them directly to a table with two empty chairs.

        Groups may share tables, however if at the same time you have an empty table with the required number of
        chairs and enough empty chairs at a larger one, you must always seat your client(s) at an empty table and
        not any partly seated one, even if the empty table is bigger than the size of the group.

        Of course the system assumes that any bigger group may get bored of seeing smaller groups arrive and get
        their tables ahead of them, and then decide to leave, which would mean that they abandon the queue without being served."
        
The program creates 10 tables of different capacity (this is done in class "Table") and then starts randomly creating groups of customers of different sizes (there is a 2 sec lag  before creating the next group; each groups has it's own id). Once a group is created, "FindingTable" class tries to seat it at a table, following challenge's rules. If it is impossible, the group stays in line, waiting for a proper table to get free. A group that is still waiting in line may (randomly) decide to give up and leave. Seated groups (again randomly) finish eating and leave, thus freeing space for other groups. All this is managed by "Group" class, which is also the entry point into the program.

In the beginning I planned to use several threads to make all events completely independent of each other time-wise, but saw that at the moment multy-threading is a little bit too much for me. So the program follows one line with time lag between creating groups. However, all events are randomized, so at each iteration different events might - or might not - happen.

At each iteration the simulator prints into the console messages about events:
- when new groups is created: "Created new group of 3 (id 58)"
- when eating group finishes and leaves: "The group with index 0 at table index 5 has finished eating and left"
- when waiting group gives up and leaves: "The group at index 3 (group of 2 (id 181)) decided not to wait for free table and has left the line"
- After that it prints state of all 10 tables after all abovementioned events were executed and tables re-sorted (table's name, how many free seats it currently has and what groups are seated at that  table, if any):

  table_01_2   Free seats 2    [[]] 

   table_07_5   Free seats 5    [[]]

   table_05_4   Free seats 0    [[group of 4 (id 153)]]

   table_02_2   Free seats 0    [[group of 2 (id 138)]]

   table_09_6   Free seats 0    [[group of 6 (id 131)]]

   table_03_3   Free seats 0    [[group of 1 (id 142), group of 2 (id 152)]]

   table_06_4   Free seats 1    [[group of 3 (id 150)]]

   table_04_3   Free seats 1    [[group of 2 (id 144)]]

   table_08_5   Free seats 1    [[group of 2 (id 151), group of 2 (id 154)]]

   table_10_6   Free seats 3    [[group of 3 (id 145)]]  
   
And in the end the current state of the line to be seated: "Currently wait in line to be seated: [[group of 6 (id 155), group of 2 (id 156)]]"


   





# 🍝 Philosophers - Concurrent Dining Problem

Welcome to my **Philosophers** repository! This project is part of the **42 curriculum**, where I implemented the classic dining philosophers problem using threads and mutexes. This project deepened my understanding of concurrency, resource sharing, and synchronization in multi-threaded applications.

---

## **✅ Project Validation**
- **Validated on:** October 16, 2024
- **Final Score:** 100/100

---

## **📜 Project Overview**
The goal of this project was to solve the dining philosophers problem - a classic synchronization challenge that illustrates the complexities of resource allocation and deadlock prevention in concurrent systems.

### **The Scenario:**
- Multiple philosophers sit at a round table with a large bowl of spaghetti in the center
- Each philosopher alternates between three states: eating, thinking, and sleeping
- While eating, they need two forks - one from their left and one from their right
- There are only as many forks as philosophers (limited shared resources)
- After eating, philosophers put down both forks and start sleeping
- After sleeping, philosophers start thinking, then try to eat again
- The simulation stops when a philosopher dies of starvation
- Philosophers must avoid dying!

### **Key Requirements:**
- Each philosopher must be a separate thread
- One fork between each pair of philosophers (protected by mutex)
- Prevent philosophers from duplicating forks
- Display state changes with precise timestamps
- Ensure philosophers don't die from starvation
- Avoid data races
- Implement proper synchronization mechanisms

### **Program Arguments:**
1. `number_of_philosophers`: Number of philosophers and forks
2. `time_to_die`: Milliseconds a philosopher can go without eating before dying
3. `time_to_eat`: Milliseconds it takes to eat (while holding two forks)
4. `time_to_sleep`: Milliseconds a philosopher spends sleeping
5. `[number_of_times_each_philosopher_must_eat]`: Optional argument - if all philosophers eat this many times, the simulation stops

---

## **🛠️ Implementation Details**

### **🧵 Multi-threading Approach**
- Created one thread per philosopher
- Used mutex locks to ensure exclusive access to forks
- Implemented careful synchronization to prevent deadlocks
- Added precise timing mechanisms for simulation accuracy

### **🔄 Philosopher States**
Each philosopher rotates through these states:
1. **Thinking**: Waiting to acquire forks
2. **Eating**: Holding two forks and consuming food (reset starvation timer)
3. **Sleeping**: Resting after eating before thinking again

### **⚙️ Key Components**
- **Mutex Protection**: Each fork is protected by a mutex to prevent simultaneous access
- **Death Monitoring**: Continuous checking if any philosopher has gone too long without eating
- **Time Management**: Precise millisecond tracking using `gettimeofday()`
- **Resource Allocation**: Strategic fork acquisition to prevent deadlocks
- **State Logging**: Thread-safe status updates with timestamps

### **🔍 Deadlock Prevention**
Implemented a key strategy to prevent deadlocks:
- Even-numbered philosophers attempt to pick up right fork first
- Odd-numbered philosophers attempt to pick up left fork first
- This breaks the circular wait condition, a necessary condition for deadlocks

---

## **📋 Compilation and Usage**

### **🔨 Compilation**
```bash
# Clone repository
git clone https://github.com/osmaneb23/42-Philosophers.git
cd 42-Philosophers

# Compile the program
make
```

### **💻 Running the Program**
```bash
./philo <number_of_philosophers> <time_to_die> <time_to_eat> <time_to_sleep> [number_of_times_each_philosopher_must_eat]
```

### **Example Usage**
```bash
# Run with 5 philosophers, 800ms time to die, 200ms to eat, 200ms to sleep
./philo 5 800 200 200

# Run with 4 philosophers, 410ms time to die, 200ms to eat, 200ms to sleep, must each eat 5 times
./philo 4 410 200 200 5
```

### **Expected Output:**
```
0 | Philosopher 1 has taken a fork
0 | Philosopher 1 has taken a fork
0 | Philosopher 1 is eating
0 | Philosopher 2 has taken a fork
200 | Philosopher 4 has taken a fork
200 | Philosopher 4 has taken a fork
200 | Philosopher 4 is eating
200 | Philosopher 1 is sleeping
200 | Philosopher 2 has taken a fork
200 | Philosopher 2 is eating
400 | Philosopher 1 is thinking
400 | Philosopher 1 has taken a fork
400 | Philosopher 3 has taken a fork
400 | Philosopher 4 is sleeping
...
```

---

## **📂 Project Structure**
```
42-Philosophers/
│── includes/
│   └── philosophers.h     # Main header file with structs and prototypes
│── src/
│   │── cleaning.c         # Memory cleanup and resource freeing
│   │── forks.c            # Fork management and synchronization
│   │── init.c             # Initialization of philosophers and mutexes
│   │── main.c             # Program entry point and argument handling
│   │── routine.c          # Main philosopher lifecycle routines
│   │── routine_utils.c    # Helper functions for philosopher routines
│   │── utils.c            # General utility functions
│   └── utils2.c           # Additional utility functions
└── Makefile               # Compilation instructions
```

---

## **🧩 Key Challenges**
- **Race Conditions**: Ensuring thread-safe access to shared resources
- **Deadlocks**: Preventing scenarios where philosophers wait indefinitely
- **Starvation**: Ensuring all philosophers get fair access to forks
- **Timing Precision**: Accurate tracking of eating, sleeping, and dying times
- **Resource Management**: Proper initialization and cleanup of threads and mutexes

---

## **🎓 Key Learning Outcomes**
- **Concurrency**: Deep understanding of multi-threading and parallel execution
- **Synchronization**: Mastery of mutex locks for resource protection
- **Thread Management**: Creating, managing, and joining threads
- **Deadlock Prevention**: Techniques to avoid circular waits and resource contention
- **Time Management**: Precise tracking of events in a concurrent environment
- **Problem Modeling**: Translating a theoretical problem into a practical implementation
- **Resource Allocation**: Efficient management of limited shared resources

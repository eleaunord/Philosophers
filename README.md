# Philosophers

> 🍝 Because even eating spaghetti can lead to deadlocks.

## 🧠 Project Overview

**Philosophers** is a concurrency project from the 42 Common Core. The goal is to simulate the classic **dining philosophers problem**, a well-known exercise in concurrent programming. Each philosopher is a thread that alternates between eating, sleeping, and thinking, and must compete with others to access shared forks (resources).

The main challenge is avoiding **deadlocks**, **race conditions**, and **starvation** using **mutexes** and proper thread synchronization.

---

## 🧵 Mandatory Part: Threads and Mutexes

In this version:

* Each philosopher is a **thread**.
* Each fork is a **mutex**.
* I had to make sure no two threads accessed the same fork at the same time.
* The simulation ends either when a philosopher **dies of starvation** or (if specified) when each has eaten a certain number of times.

### Allowed functions:

* `pthread_create`, `pthread_mutex_lock`, `usleep`, `gettimeofday`, etc.

---

## 🧠 What I Learned

### Thread Synchronization

* I learned to use `pthread_create`, `pthread_mutex_lock`, `pthread_join`, and related functions to manage thread behavior and access to shared data safely.

### Mutex Logic

* I now understand how mutexes prevent concurrent access to critical sections — like forks in this simulation — and how poor use of mutexes can lead to deadlocks.

### Precise Timing

* Using `gettimeofday()` and `usleep()`, I implemented millisecond-accurate timing to detect when a philosopher should die or move to the next action.

### Deadlock Avoidance

* I used different strategies like having odd and even philosophers pick up forks in opposite orders to avoid all of them waiting on each other.

---

## 😓 Challenges I Faced

### Deadlocks

Early on, all philosophers would grab the left fork and then wait forever on the right — classic deadlock. I had to think carefully about the order of actions and how to desynchronize threads slightly to avoid it.

### Race Conditions

Sometimes, philosophers would access shared data (like time since last meal) at the same time, leading to undefined behavior. Adding mutexes in the right places took trial and error.

### Philosopher Death Timing

Ensuring a philosopher died **exactly when they should** — and that the death message appeared within **10 ms** — was one of the hardest parts. It pushed me to improve my understanding of time measurement and thread responsiveness.

---

## 🧪 How to Run

### Compile:

```bash
make
```

### Run simulation:

```bash
./philo 5 800 200 200
```

Arguments:

1. Number of philosophers
2. Time to die (ms)
3. Time to eat (ms)
4. Time to sleep (ms)
5. (optional) Number of times each philosopher must eat

---

## 💡 Example Output

```
0 1 is thinking
1 2 has taken a fork
2 2 has taken a fork
3 2 is eating
...
500 3 died
```

## ✅ Final Thoughts

This project was my first serious dive into **multithreading** and **concurrency** in C. It was both frustrating and fascinating. I now understand how timing, synchronization, and shared data can cause real-world problems like deadlocks and starvation. It’s made me a more careful and structured programmer — and gave me a huge appreciation for systems programming.

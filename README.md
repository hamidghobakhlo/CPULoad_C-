# CPU Load Calculation Program in C++

This program is written in C++ and its purpose is to calculate the CPU load percentage in a Windows operating system. Below is a detailed explanation of each part of the code:

## General Overview:
- The program uses the `GetSystemTimes` function from the Windows API to retrieve various times related to CPU usage, such as idle time, kernel time, and user time.
- It then calculates the CPU load percentage based on these times.
- The CPU load is calculated as the percentage of time the CPU has been actively processing tasks, excluding idle time.

## Breakdown of the Program:

### 1. Libraries and Headers:
- `#include <iostream>`: Used for input/output functions like `printf`.
- `#include "windows.h"`: Used for Windows-specific functions and structures such as `FILETIME` and `GetSystemTimes`.
- `#include "stdlib.h"`: Includes general-purpose functions like `malloc` or `free` (not used in this code but typically included for memory management).
- `#include "Winnetwk.h"`: Provides access to Windows networking functions, although it is not used in this specific code. It might be included for other purposes.

### 2. Functions:
- `static float CalculateCPULoad(unsigned long long, unsigned long long);`: This function calculates the CPU load based on the time spent in idle and active states.
- `static unsigned long long FileTimeToInt64(const FILETIME&);`: This function converts the `FILETIME` structure to an `unsigned long long` integer so it can be processed.
- `float GetCPULoad();`: This function retrieves the CPU load percentage.

### 3. Program Logic:

#### Calculating the CPU Load (`GetCPULoad`):
- The `GetSystemTimes` function is called to get the idle time, kernel time, and user time of the CPU, in the form of `FILETIME` structures.
- These `FILETIME` values are then converted to `unsigned long long` integers using the `FileTimeToInt64` function.
- The `CalculateCPULoad` function is then used to compute the CPU load based on these converted values.

#### Calculating CPU Load Percentage (`CalculateCPULoad`):
- This function calculates the CPU load by comparing the differences in idle and total times (the sum of idle, kernel, and user times) from the previous and current time intervals.
- If there is no change in the time values (for instance, if the CPU is idle), the CPU load is considered to be 0%.

#### Converting `FILETIME` to `unsigned long long` (`FileTimeToInt64`):
- The `FileTimeToInt64` function converts a `FILETIME` structure, which consists of two 32-bit values (`dwLowDateTime` and `dwHighDateTime`), into a single 64-bit value of type `unsigned long long`.
- This conversion allows the times to be easily processed for calculation.

### 4. Static Variables:
- `_previousTotalTicks` and `_previousIdleTicks` are static variables that store the previous CPU usage times. These variables are used to calculate the difference between the current and previous times, which is essential for calculating the CPU load.

### 5. Output:
- After calculating the CPU load, the result is printed to the console as a percentage using the `printf` function.

## Conclusion:
This program effectively and efficiently measures the CPU load on a Windows system. By using Windows API functions to retrieve CPU times and converting them into processable data, the program calculates the CPU load percentage, which is useful for monitoring system performance.

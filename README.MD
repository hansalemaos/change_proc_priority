# A flexible and convenient solution for managing process priorities - Windows only

## pip install change-proc-priority

#### Tested against Windows 10 / Python 3.10 / Anaconda


This module offers a flexible and convenient solution for managing process priorities, making it valuable for system administrators, performance optimizers, developers, and researchers who need to fine-tune resource allocation and optimize system performance



### Process Priority Control: 

The module provides functionality to monitor and change the priority of processes running on a system. 
This can be useful in scenarios where fine-tuning the priority of specific processes can have a 
significant impact on system performance or resource allocation.

### Constant Monitoring: 

The constant_check_and_change_priority function allows for continuous monitoring of processes, 
ensuring that the desired priority is maintained even if processes are created or terminated dynamically.

### Regular Expression Support: 

The module supports using regular expressions to specify the executable path of the target processes. 
This provides flexibility in defining patterns and allows for more complex matching criteria.

### CLI and Function Interface: 

The module can be utilized both through the command line interface (CLI) and by directly calling the constant_check_and_change_priority function in Python code. 
This provides versatility in how the module can be incorporated into different workflows and automation processes.

### Customizable Parameters: 

The module allows for customization of various parameters such as priority, delay between checks, and the ability to close the program after the first matching process is found. 
This flexibility enables users to tailor the behavior of the module according to their specific requirements.


```python
constant_check_and_change_priority(
    exe_path: str | None = None,
    priority: int = NORMAL,
    is_regex: int | bool = 1,
    flags: int = re.I,
    delay: float | int = 1.0,
    close_after_first: int | bool = 0,
):
    r"""
    Constantly checks and changes the priority of processes based on the provided parameters.

    Args:
        exe_path (str | None): Path or regular expression pattern of the executable to monitor.
        priority (int): Priority value to set for the processes. Valid options are:
            - LOW = 64
            - BELOW_NORMAL = 16384
            - NORMAL = 32
            - ABOVE_NORMAL = 32768
            - HIGH = 128
            - REALTIME = 256
            Defaults to NORMAL (32).
        is_regex (int | bool): Flag indicating whether the exe_path should be treated as a regular expression pattern.
            Defaults to 1 (True).
        flags (int): Flags to be used with the regular expression pattern. Defaults to re.I (ignore case).
        delay (float | int): Delay in seconds between each check. Defaults to 1.0.
        close_after_first (int | bool): Flag indicating whether to exit the program after the first process is found.
            Defaults to 0 (False).

    Returns:
        Callable: A function that can be used to stop the monitoring thread.

    Example:
        Changing priority of one process - function call:
        This line shows an example of calling the change_priority function to change the priority of a specific process
        with a given PID. In this case, the priority is set to HIGH. The PID used here is 21360.

        change_priority(pid=21360,priority=HIGH)
        #################################################
        Constantly changing priority of processes with exe_path - CLI:
        This line demonstrates how to use the script from the command line interface (CLI)
        to constantly monitor and change the priority of processes based on the specified exe_path parameter.
        The script is invoked using the python command, followed by the script path.
        The CLI arguments are provided using -- followed by the argument name and its corresponding value.
        In this example, the exe_path is set to notepad.exe$, the priority is set to 128 (which corresponds
        to HIGH priority), is_regex is set to 1 (True), flags is set to 2, delay is set to 2.0 seconds,
        and close_after_first is set to 0 (False).

        # adjust the path!
        python "C:\ProgramData\anaconda3\envs\dfdir\Lib\site-packages\change_proc_priority\__init__.py" --exe_path notepad.exe$ --priority 128 --is_regex 1 --flags 2 --delay 2.0 --close_after_first 0
        #################################################


        This part showcases an example of using the constant_check_and_change_priority function directly in Python code.
        The function is called with various parameters to monitor and change the priority of processes.
        In this example, the exe_path is set to "notepad.exe$", indicating a regular expression pattern,
        the priority is set to NORMAL, is_regex is set to True, flags is set to re.I (ignore case),
        delay is set to 1.0 second, and close_after_first is set to False.
		
		from change_proc_priority import constant_check_and_change_priority
        stop_monitoring=constant_check_and_change_priority(
        exe_path="notepad.exe$",
        priority=NORMAL,
        is_regex=True,
        flags=re.I,
        delay=1.0,
        close_after_first=False,
        )
        #################################################

        # To stop the monitoring thread, call the returned function
        stop_monitoring()
    """
```

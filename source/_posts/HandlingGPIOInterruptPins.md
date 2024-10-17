---
title: Handling GPIO InterruptPins
date: 2024-10-17 16:13:30
tags:
---

## Steps to Read and Configure GPIOs with Interrupts

### 1. Access GPIO Pins via `sysfs` Interface

In Linux, the **sysfs** interface allows access to GPIO pins. The following steps will help you list and configure GPIOs.

- List Available GPIOs:

  - In most cases, GPIO pins are mapped under `/sys/class/gpio`.

  - First, check if the GPIOs are exported by looking at this directory:

    ```sh
    ls /sys/class/gpio/
    ```

- Export a GPIO Pin:

  - If a GPIO pin is not visible, export it by writing its number into the `export` file.

    ```sh
    echo <GPIO_PIN_NUMBER> > /sys/class/gpio/export
    ```

  - For example, to export GPIO pin 22:

    ```sh
    echo 22 > /sys/class/gpio/export
    ```

- Check GPIO Pin Direction:

  - After exporting the pin, check or configure the GPIO direction (input or output) by interacting with the `direction` file.

    ```sh
    cat /sys/class/gpio/gpio22/direction
    ```

  - To set the GPIO as an input pin (necessary for interrupt):

    ```sh
    echo "in" > /sys/class/gpio/gpio22/direction
    ```

### 2. Enable GPIO Interrupts

Once a GPIO pin is exported, you can configure its edge detection, which enables the interrupt functionality.

- Set the Interrupt Trigger:

  - You can configure which edge (voltage change) the GPIO will respond to by writing to the `edge` file. Possible values include:

    - `none`: No interrupt (default).
    - `rising`: Trigger on rising edge (low to high).
    - `falling`: Trigger on falling edge (high to low).
    - `both`: Trigger on both edges (rising and falling).

  - For example, to trigger on both rising and falling edges:

    ```sh
    echo "both" > /sys/class/gpio/gpio22/edge
    ```

### 3. Monitor GPIO Interrupt Events

- A more practical approach for real-time monitoring is to use the `poll()` system call in a C or Python program. Alternatively, you can use `inotifywait` in a terminal to monitor changes.

- To use `inotifywait`:

  ```sh
  sudo apt-get install inotify-tools
  ```

  ```sh
  inotifywait -m /sys/class/gpio/gpio22/value
  ```

- This will display a notification whenever the value of the GPIO changes, i.e., when an interrupt occurs.

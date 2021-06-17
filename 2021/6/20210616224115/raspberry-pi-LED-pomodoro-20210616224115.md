|  Title | Category  | Tags  | Date |
| ------------ | ------------ | ------------ | ----|
| raspberry-pi-LED-pomodoro | project  | raspberry pi, project, pomodoro  | 20210616224115 |

# raspberry pi LED pomodoro
I had an idea to make a Raspberry Pi project that would control lights in my office
using a Raspberry Pi Zero.

## Structure
* Have a Raspberry Pi tied to an LED light strip
* Run a custom `socketserver` that accepts commands from a remote local server
* Have an LED control program that would handle a pomodoro configuration

## Pomodoro setup
* Red - working period
* Yellow - break period
* Green - Free time


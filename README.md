# -VEX-Robot-Project
from pathlib import Path

code = """from vex import *

# --------------------
# Setup
# --------------------

brain = Brain()

left_motor = Motor(Ports.PORT1, GearSetting.RATIO_1_1, False)
right_motor = Motor(Ports.PORT6, GearSetting.RATIO_1_1, True)
spinner_motor = Motor(Ports.PORT3, GearSetting.RATIO_1_1, False)

drivetrain = DriveTrain(left_motor, right_motor)

spinner_motor.set_velocity(100, PERCENT)
drivetrain.set_drive_velocity(60, PERCENT)

# --------------------
# Functions
# --------------------

def collect_and_filter():
    drivetrain.drive(FORWARD)
    wait(2, SECONDS)
    drivetrain.stop()
    
    spinner_motor.spin_for(FORWARD, 360, DEGREES)
    wait(0.5, SECONDS)

def turn_right():
    drivetrain.turn_for(RIGHT, 90, DEGREES)

def turn_left():
    drivetrain.turn_for(LEFT, 90, DEGREES)

def move_forward_time(t):
    drivetrain.drive(FORWARD)
    wait(t, SECONDS)
    drivetrain.stop()

# --------------------
# Start Message
# --------------------

brain.screen.print("Press LEFT to start")

while not brain.buttonLeft.pressing():
    wait(10, MSEC)

brain.screen.clear_screen()
brain.screen.print("Running...")

# --------------------
# Main Loop
# --------------------

while True:
    
    collect_and_filter()
    move_forward_time(1.5)
    turn_right()
    move_forward_time(1)
    turn_right()
    
    collect_and_filter()
    move_forward_time(1.5)
    turn_left()
    move_forward_time(1)
    turn_left()
"""

path = Path("/mnt/data/VEX_Robot_Project.py")
path.write_text(code, encoding="utf-8")

str(path)

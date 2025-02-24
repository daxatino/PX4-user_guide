# vehicle_status (UORB message)



[source file](https://github.com/PX4/PX4-Autopilot/blob/main/msg/vehicle_status.msg)

```c
uint64 timestamp				# time since system start (microseconds)

uint8 ARMING_STATE_INIT = 0
uint8 ARMING_STATE_STANDBY = 1
uint8 ARMING_STATE_ARMED = 2
uint8 ARMING_STATE_STANDBY_ERROR = 3
uint8 ARMING_STATE_SHUTDOWN = 4
uint8 ARMING_STATE_IN_AIR_RESTORE = 5
uint8 ARMING_STATE_MAX = 6

# FailureDetector status
uint16 FAILURE_NONE = 0
uint16 FAILURE_ROLL = 1              # (1 << 0)
uint16 FAILURE_PITCH = 2             # (1 << 1)
uint16 FAILURE_ALT = 4               # (1 << 2)
uint16 FAILURE_EXT = 8               # (1 << 3)
uint16 FAILURE_ARM_ESC = 16          # (1 << 4)
uint16 FAILURE_BATTERY = 32          # (1 << 5)
uint16 FAILURE_IMBALANCED_PROP = 64  # (1 << 6)
uint16 FAILURE_MOTOR = 128           # (1 << 7)

# HIL
uint8 HIL_STATE_OFF = 0
uint8 HIL_STATE_ON = 1

# Navigation state, i.e. "what should vehicle do".
uint8 NAVIGATION_STATE_MANUAL = 0		# Manual mode
uint8 NAVIGATION_STATE_ALTCTL = 1		# Altitude control mode
uint8 NAVIGATION_STATE_POSCTL = 2		# Position control mode
uint8 NAVIGATION_STATE_AUTO_MISSION = 3		# Auto mission mode
uint8 NAVIGATION_STATE_AUTO_LOITER = 4		# Auto loiter mode
uint8 NAVIGATION_STATE_AUTO_RTL = 5		# Auto return to launch mode
uint8 NAVIGATION_STATE_UNUSED3 = 8 	        # Free slot
uint8 NAVIGATION_STATE_UNUSED = 9	        # Free slot
uint8 NAVIGATION_STATE_ACRO = 10		# Acro mode
uint8 NAVIGATION_STATE_UNUSED1 = 11		# Free slot
uint8 NAVIGATION_STATE_DESCEND = 12		# Descend mode (no position control)
uint8 NAVIGATION_STATE_TERMINATION = 13		# Termination mode
uint8 NAVIGATION_STATE_OFFBOARD = 14
uint8 NAVIGATION_STATE_STAB = 15		# Stabilized mode
uint8 NAVIGATION_STATE_UNUSED2 = 16		# Free slot
uint8 NAVIGATION_STATE_AUTO_TAKEOFF = 17	# Takeoff
uint8 NAVIGATION_STATE_AUTO_LAND = 18		# Land
uint8 NAVIGATION_STATE_AUTO_FOLLOW_TARGET = 19	# Auto Follow
uint8 NAVIGATION_STATE_AUTO_PRECLAND = 20	# Precision land with landing target
uint8 NAVIGATION_STATE_ORBIT = 21       # Orbit in a circle
uint8 NAVIGATION_STATE_AUTO_VTOL_TAKEOFF = 22   # Takeoff, transition, establish loiter
uint8 NAVIGATION_STATE_MAX = 23

uint8 VEHICLE_TYPE_UNKNOWN = 0
uint8 VEHICLE_TYPE_ROTARY_WING = 1
uint8 VEHICLE_TYPE_FIXED_WING = 2
uint8 VEHICLE_TYPE_ROVER = 3
uint8 VEHICLE_TYPE_AIRSHIP = 4

# state machine / state of vehicle.
# Encodes the complete system state and is set by the commander app.

uint8 nav_state				# set navigation state machine to specified value
uint64 nav_state_timestamp              # time when current nav_state activated
uint8 arming_state			# current arming state
uint8 hil_state				# current hil state
bool failsafe				# true if system is in failsafe state (e.g.:RTL, Hover, Terminate, ...)
uint64 failsafe_timestamp               # time when failsafe was activated

uint8 system_type			# system type, contains mavlink MAV_TYPE
uint8 system_id			# system id, contains MAVLink's system ID field
uint8 component_id			# subsystem / component id, contains MAVLink's component ID field

uint8 vehicle_type          # Type of vehicle (rotary wing/fixed-wing/rover/airship, see above)
                            # If the vehicle is a VTOL, then this value will be VEHICLE_TYPE_ROTARY_WING while flying as a multicopter,
                            # and VEHICLE_TYPE_FIXED_WING when flying as a fixed-wing

bool is_vtol				# True if the system is VTOL capable
bool is_vtol_tailsitter                 # True if the system performs a 90° pitch down rotation during transition from MC to FW
bool in_transition_mode			# True if VTOL is doing a transition
bool in_transition_to_fw		# True if VTOL is doing a transition from MC to FW

bool rc_signal_lost				# true if RC reception lost

bool data_link_lost				# datalink to GCS lost
uint8 data_link_lost_counter			# counts unique data link lost events

bool high_latency_data_link_lost 			# Set to true if the high latency data link (eg. RockBlock Iridium 9603 telemetry module) is lost

bool mission_failure				# Set to true if mission could not continue/finish
bool geofence_violated

uint16 failure_detector_status			# Bitmask containing FailureDetector status [0, 0, 0, 0, 0, FAILURE_ALT, FAILURE_PITCH, FAILURE_ROLL]

# see SYS_STATUS mavlink message for the following
# lower 32 bits are for the base flags, higher 32 bits are or the extended flags
uint64 onboard_control_sensors_present
uint64 onboard_control_sensors_enabled
uint64 onboard_control_sensors_health


uint8 ARM_DISARM_REASON_TRANSITION_TO_STANDBY = 0
uint8 ARM_DISARM_REASON_RC_STICK = 1
uint8 ARM_DISARM_REASON_RC_SWITCH = 2
uint8 ARM_DISARM_REASON_COMMAND_INTERNAL = 3
uint8 ARM_DISARM_REASON_COMMAND_EXTERNAL = 4
uint8 ARM_DISARM_REASON_MISSION_START = 5
uint8 ARM_DISARM_REASON_SAFETY_BUTTON = 6
uint8 ARM_DISARM_REASON_AUTO_DISARM_LAND = 7
uint8 ARM_DISARM_REASON_AUTO_DISARM_PREFLIGHT = 8
uint8 ARM_DISARM_REASON_KILL_SWITCH = 9
uint8 ARM_DISARM_REASON_LOCKDOWN = 10
uint8 ARM_DISARM_REASON_FAILURE_DETECTOR = 11
uint8 ARM_DISARM_REASON_SHUTDOWN = 12
uint8 ARM_DISARM_REASON_UNIT_TEST = 13

uint8 latest_arming_reason
uint8 latest_disarming_reason

uint64 armed_time       # Arming timestamp (microseconds)

uint64 takeoff_time     # Takeoff timestamp (microseconds)

bool safety_button_available # Set to true if a safety button is connected
bool safety_off # Set to true if safety is off

```

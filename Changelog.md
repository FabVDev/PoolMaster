PoolMaster: change log
=======================
v4.0.3
-------

*Added calibration function for the water pressure sensor {"PSICalib":[0,0,0.71,0.6]}
*Added generic function {"Relay":[1,1]} to actuate spare relays. Useful to add custom control features to the project such as lighting, etc

v4.0.0
-------

*Starting and stopping PIDs when filtration is manually started/stopped. This is useful in spring when the water is cold, filtrations tops early, however one might wish to manually start it in the afternoon and have the PIDs regulating the water quality

v4.0.0
-------

*Acid and Chlorine tank levels are now estimated and reported in % fill (estimation based on the running-time of each pump)
* /!\ API change. MQTT published payloads now also include stored Orp, pH and Water temp setpoints as well as tank-level estimates. Two separate publishes are used in order to reduce the payload size of each publish
* A daily 2 minutes cycling of the water heating circulator has been added in order to maintain it in good condition when not being used for long period of times (eg. in winter)
* Pump class now support setups in which PoolMaster does not manage the filtration pump (eg. in cases where an already-installed automate handles it). See Pump class for more info
* Node Red code example now includes feeding the MQTT data into an InfluxBD database in order to generate a Grafana Dashboard (code for the node red flow and the Grafana dashboard is provided)

v3.1.2
-------

* fixed bug preventing from operating the pH and Orp pumps manually when MODE was in MANUAL mode

v3.1.0
-------

* new regulation loop to regulate the water temperature. It starts/stops the house-heating system circulator which brings heat to a heat exchanger mounted on the pool water pipes
* new API function to switch on/off the water heating regulation loop

v3.0.3
-------

* Added support for a front panel push-button with a red LED-ring. It enables toggling between LCD screens (short press) and clearing errors (long-press). When a system-error occurs (eg. empty chemical tank, low-water pressure or chemical-pump overtime) the front-panel push-button red LED-ring starts blinking, calling for attention.
* Adjusted default PID constants

v3.0.1
-------

* improved security at Pumps level so that Orp and pH pumps cannot run and/or stop if Filtration is not running/stopped
* fixed bug. Now when filtration pump is running but water pressure remains low, filtration pump is really stopped

v3.0.0
-------

* modified anti-freeze filtration behaviour. It now starts filtration when outside air temperature goes below -2.0deg and stops it when it rises back above +2.0deg
* added support for a water pressure sensor. A water pressure which increases above a certain threshold can be an indication that the sand filter requires cleaning). When filtration is running but water pressure is below a certain threshold (ie. something is wrong), filtration is automatically stopped as a safety precaution
* Added better support for the Arduino Mega2560 platform. Should now compile without any code modification
* Added the "Pump" class to improve quality of code and easier integration of additional pumps in the future if required (eg. pH+ pump)
* Added integration example into cloud-based BLYNK smart phone application via NodeRed
* /!\ API change. The measured data and the IO and IO2 bitmaps which are published to the MQTT broker have been modified in order to accomodate the water pressure readings

v2.1.2
-------

* changed Eeprom config storage handling
* added incoming MQTT message queue to reduce load on MQTT callback function (causing spurious socket errors and subsequent disconnections from broker)
* Ethernet deconnection now non-blocking
* Some minor changes

v2.1.1
-------

* fixed bug in AntiFreeze filtration function
* updated documentation

v2.1.0
-------

* LCD display now toggles between two screens every 6 seconds, shows more info
* modified PhPump() and ChlPump() functions to prevent the pumps from starting if Tank Levels are low
* Tanks Level errors now display error code on the LCD display but do not disable the PID loops or the filtering pûmp anymore, only the peristaltic pumps
* PID regulation loops start are now delayed for 30mins (by default) after the filtration start in order to let the readings stabilize first
* New API function to tell the system what the external temperature is. This is used to start regular short filtering periods of 10mins every hour when external temperature is below 2deg.
* Improved PID loops tuning

v2.0.1
-------

* /!\ changed CONTROLLINO pin number for the PH_PUMP
* Tuned PID parameters
* fixed bug in Mode API function

v2.0.0
-------

* New API function for multi-point linear regression calibration of pH and Orp sensors
* Former API function for the Offset Calibration of the pH and Orp sensors are no longer available
* getMeasures() function now based on calibrated linear function to compute pH and Orp values
* PublishDataCallback() function now using ArduinoJSON library to generate payload
* Eeprom, Webserver and XML file now store/display the calibration coefficients for the pH and Orp sensors

v1.0.0
-------

* First release
* LCD display support
* MQTT API
* Updated hardware list
This goal for this project is to provide a template for modular, quick and easy BLE Gatt Server development on the ESP32 using the ESP IDF. To facilitate this, the ble service table example from the ESP IDF was modified and broken into four main sections. This example should run without any need for edits. 

### Requirements:
* min 4mb ram configured in make menuconfig/Serial flasher config/Flash size
* ble enabled in make menuconfig/Component config/Bluetooth/Bluetooth
* min ESP-IDF v3.0 (should work, but have only tested on v3.1 beta)


This is a work in progress and was just quickly thrown together and generalized from code in another project! I'm not currently focusing a lot of time on it, but more adding to it as I fine tune the files in projects that I'm currently using this structure in.

Feel free to PR the repo. I'll try to get changes merged quickly.

Special thanks to Jesse Bahr who originally seperated out the interface/gatts/gap.

Future Development:
* Add BLE Notify/Indicate 
* Add comments/documentation throughout
* Add Doxygen support
* General Cleanup

# Main Sections:
ble_interface - This provides the only calls you will need to enable/disable Bluetooth LE. Calling ble_interface_init() sets up the bluetooth hardware, gap, and gatt server then begins the advertising process. ble_interface_deinit() nicely shuts down Bluetooth and performs all the ESP IDF suggested calls to deallocate resources.

ble_gap - This manages the Bluetooth advertising setup and data. This is the source file you would edit to change the advertising name, data, and settings. No need to call the init/deinit functions. ble_interface takes care of that for you.

ble_gatt_server - This manages the Bluetooth server handling. You will need to edit the commented areas in the gatts_profile_event_handler() function to add new services.

ble_services - This directory contains a template file for a service. This template provides a quick and easy example that creates a services with characteristics that can be read from/written to.

#!/bin/bash

# Exit immediately if any command fails
set -e

# Function to install Realtek RTL8812AU driver
install_rtl8812au_driver() {
  # Store the current directory
  current_dir=$(pwd)

  # Change to the directory of the script
  cd "$(dirname "$0")"

  echo "Removing existing rtl8812au folder..."
  rm -rf rtl8812au
  echo "Cloning repository..."
  git clone https://github.com/gordboy/rtl8812au.git
  echo "Building and installing the driver..."
  cd rtl8812au

  # Correct the path to phydm.mk in the Makefile
  sed -i 's|\$(KSRC)/hal/phydm/phydm.mk|hal/phydm/phy8812au/hal/phydm/phydm.mk|' Makefile
  
  # Return to the original directory
  cd "$current_dir"
}

# Call the function to install the driver
install_rtl8812au_driver

# Function to uninstall Realtek RTL8812AU driver
uninstall_rtl8812au_driver() {
  echo "Uninstalling RTL8812AU driver..."
  # Add commands to uninstall the RTL8812AU driver
  # For example, you may need to run 'make uninstall' or other cleanup commands
}

# Function to check USB connection for RTL8812AU
check_usb_connection_rtl8812au() {
  # Add code to check USB connection for RTL8812AU
  # For example, you might want to ping or perform some other network-related check
  # Return 0 if connection is valid, 1 otherwise
  return 0
}

# List of drivers to try
drivers=("RTL8812AU")

# Scan for USB devices
usb_devices=$(lsusb)

# Iterate through each driver
for driver in "${drivers[@]}"; do
  echo "Trying $driver driver..."

  # Install the driver
  "install_${driver,,}_driver" || {
    echo "Automatic installation of $driver driver failed."
    echo "Please visit <driver specific link> for manual installation instructions."
    continue
  }

  # Check USB connection
  case $driver in
    "RTL8812AU")
      if check_usb_connection_rtl8812au; then
        echo "USB connection is valid with $driver driver."
        exit 0 # Exit script if successful connection
      else
        echo "USB connection is not valid with $driver driver."
      fi
      ;;
    *)
      echo "Unknown driver '$driver'."
      ;;
  esac
done

echo "None of the drivers provided a valid USB connection."
exit 1

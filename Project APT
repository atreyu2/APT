import os
import time
import datetime
from datetime import datetime
import sys

# Function to get information about files and directories in the specified folder
def get_file_info(directory):
    file_info = {}# Dictionary to store file paths and their last modification time

    # Walk through the directory, gathering information about files and folder
    for dirpath,dirnames, filenames in os.walk(directory):

         # Collect information for each file
        for filename in filenames:
            file_path = os.path.join(dirpath,filename) #Get the full file path
            mod_time=os.stat(file_path).st_mtime   # Get the last modified time of the file
            file_info[file_path]= mod_time  # Store file path and modification time in the dictionary
        
        # Collect information for each folder
        for dirname in dirnames:
            dir_path = os.path.join(dirpath, dirname) # Get the full directory path
            dir_mod_time = os.stat(dir_path).st_mtime # Get the last modified time of the directory
            file_info[dir_path] = dir_mod_time  # Store directory path and modification time

    return file_info  # Return the dictionary of files and their modification times

# This function will gather the list of files in the directory and return a dictionary
# where the key is the file/folder path and the value is the last modification time.


# Function to monitor the directory for any changes (new, modified, or deleted files)
def monitor_directory(directory,interval=10):
    print(f'monitoring changes in directory...')  # Notify the user that monitoring has started
    previous_files = get_file_info(directory)  # Take the initial snapshot of the directory

    while True:
        time.sleep(interval) # Wait for the specified interval before checking again
        current_files = get_file_info(directory) # Get the current snapshot of the directory
        
        # Check for new or modified files
        for file_path,mod_time in current_files.items():
            if file_path not in previous_files:
                print(f'new file added: {file_path}')   # Notify about any new file added
            elif mod_time != previous_files[file_path]:
                print(f'File modified:{file_path}, Last modified at: {datetime.fromtimestamp(mod_time)}') # Notify about file modifications
         
         # Check for deleted files
        for file_path in previous_files.keys():
            if file_path not in current_files:
                print(f'file deleted: {file_path}') # Check for deleted files

        previous_files = current_files # Update the previous snapshot to the current state


#__main__

if __name__ == '__main__':
    now = datetime.now() # Get the current date and time
    print('Current data and time:',now) # Print the current date and time

    # Prompt the user to start monitoring or exit the program
    while True:
        go_p = input('Would you like to start, yes or no?: ').lower() # Ask user input
        if go_p == 'yes': 
            if go_p.isalpha():# Check if the input is alphabetic (not numbers or special characters)
                break # Start monitoring
            else:
                print('That is not a valid input') # Warn if input is invalid
        else:
            print('Would you like to exit?') # Ask if they want to exit the program
            sys.exit()  # Exit the program

# Get the current working directory (folder to monitor)
directory_to_monitor = os.getcwd()
print(f'Monitoring directory: {directory_to_monitor}')# Print the directory being monitored

# Try to start monitoring the directory, stop if the user interrupts with a keyboard signal
try:
    monitor_directory(directory_to_monitor,interval=10)  # Start monitoring the directory every 10 seconds
except KeyboardInterrupt:
    print('\nMonitoring stopped by user.') # Gracefully stop the monitoring when interrupted 
    sys.exit(0)# Exit the program 

    

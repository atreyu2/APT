# Directory Monitor

A Python script that monitors a directory for file and folder changes in real-time, detecting new files, modifications, and deletions.

## Description

This tool continuously watches a specified directory and reports any changes including:
- New files or folders added
- Existing files or folders modified
- Files or folders deleted

The monitor runs in the background and provides timestamped notifications whenever changes are detected.

## Features

- **Real-time monitoring** - Detects changes as they happen
- **Comprehensive tracking** - Monitors both files and directories
- **Modification timestamps** - Shows when files were last modified
- **Recursive scanning** - Monitors all subdirectories within the target folder
- **User-friendly** - Simple prompts and clear output messages
- **Graceful exit** - Can be stopped cleanly with Ctrl+C

## Requirements

- Python 3.x
- Standard library modules (no external dependencies):
  - `os`
  - `time`
  - `datetime`
  - `sys`

## Installation

1. Clone this repository:
```bash
git clone https://github.com/yourusername/directory-monitor.git
cd directory-monitor
```

2. No additional installation required - uses Python standard library only!

## Usage

1. Navigate to the directory you want to monitor:
```bash
cd /path/to/directory/to/monitor
```

2. Run the script:
```bash
python directory_monitor.py
```

3. Follow the prompts:
   - The script will display the current date and time
   - Enter `yes` to start monitoring
   - Enter `no` to exit

4. The script will check for changes every 10 seconds by default

5. To stop monitoring, press `Ctrl+C`

## Example Output

```
Current data and time: 2026-02-07 14:30:45.123456
Would you like to start, yes or no?: yes
Monitoring directory: /home/user/documents
monitoring changes in directory...
new file added: /home/user/documents/report.txt
File modified: /home/user/documents/data.csv, Last modified at: 2026-02-07 14:31:20
file deleted: /home/user/documents/old_file.txt
```

## How It Works

1. **Initial Snapshot** - Takes a snapshot of all files and directories with their modification times
2. **Periodic Checking** - Every 10 seconds, creates a new snapshot
3. **Comparison** - Compares the new snapshot with the previous one
4. **Reporting** - Reports any differences found:
   - Files in new snapshot but not in old = New files
   - Files with different modification times = Modified files
   - Files in old snapshot but not in new = Deleted files

## Configuration

You can modify the monitoring interval by changing the `interval` parameter:

```python
monitor_directory(directory_to_monitor, interval=10)  # Check every 10 seconds
```

To monitor a specific directory instead of the current working directory, modify:

```python
directory_to_monitor = "/path/to/your/directory"  # Instead of os.getcwd()
```

## Use Cases

- **Development** - Monitor log files or output directories during testing
- **Data Processing** - Track when new data files arrive in a folder
- **Backup Verification** - Ensure backup processes are completing
- **Security** - Monitor critical directories for unauthorized changes
- **File Synchronization** - Track when files are synced or updated

## Limitations

- The script checks at fixed intervals (default: 10 seconds), so very rapid changes might be missed between checks
- Does not track changes made during the interval between checks
- Monitors the entire directory tree, which could be resource-intensive for very large directories

## Contributing

Contributions are welcome! Please feel free to submit a Pull Request.

## License

This project is open source and available under the [MIT License](LICENSE).

## Author

Your Name - [@yourusername](https://github.com/yourusername)

## Acknowledgments

- Built using Python's standard library
- Inspired by the need for simple, dependency-free file monitoring

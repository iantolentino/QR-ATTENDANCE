# QRCode Attendance Scanner

QRCode Attendance Scanner is a simple desktop application for managing attendance through QR code scanning. The program records when a user "checks in" and "checks out" using scanned QR codes and logs the attendance data in an Excel workbook. Each session is uniquely identified, and new data blocks are inserted at the top of the workbook without deleting previous records.

## Features

- **QR Code Scanning:** Accepts input of the form `Name: <Name>, ID: <IDNumber>` from a QR code.
- **Time Recording:** Automatically logs "Time In" and "Time Out" for each individual per day.
- **Live GUI Table:** Displays today's attendance records in a simple Tkinter TreeView.
- **Session Management:** Uses unique session IDs to ensure each run of the program writes its own block in the Excel file.
- **Excel Logging:** Attendance data is saved into an Excel workbook (`attendance_copy.xlsx`) in the directory `C:\AttendanceSystem\daily_data`, where new sessions are stacked at the top without overriding older data.
- **Audible Notifications:** Plays beep sounds for different events (check-in, check-out, or repeated scans).

## Requirements

- **Python 3.x**
- **Tkinter:** Usually comes with Python.
- **openpyxl:** For Excel file handling.  
  Install with:
  ```bash
  pip install openpyxl
  ```
- **winsound:** (Windows only) for beep sound functionality.

## Installation

1. **Clone or Download the Repository:**

   ```bash
   git clone https://your-repository-url.git
   cd your-repository-folder
   ```

2. **Install Dependencies:**

   Make sure you have `openpyxl` installed:
   ```bash
   pip install openpyxl
   ```

   (Tkinter and winsound are included with Python on Windows.)

## Usage

1. **Run the Application:**

   Launch the program using Python:
   ```bash
   python your_scanner_script.py
   ```

2. **Scanning:**

   - Align the QR code within the camera view.
   - The expected QR code data format is:
     ```
     Name: John Doe, ID: 123
     ```
   - Press **Enter** to process the scan.
   - The application will record the "Time In" if no record exists for the day for that user. If a record exists without a "Time Out," it will record "Time Out."
   - A beep sound will play to indicate the event, and a notification appears in the interface.

3. **Excel Logging:**

   - Each session (when you open the scanner) gets a unique header that is recorded along with the timestamp.
   - The attendance data is saved in the Excel file at:
     ```
     C:\AttendanceSystem\daily_data\attendance_copy.xlsx
     ```
   - New session data is inserted at the top, while previous sessions' data remain untouched.

## Code Overview

- **GUI Setup:**  
  The UI is built using Tkinter. The interface includes a label for instructions, a live date/time display, an input field for QR code scanning, a TreeView to display today's records, and a notification label.

- **Session Management:**  
  Each session gets a unique identifier based on the timestamp when the application starts. This ID is used as a marker in the Excel file to ensure each run produces a single, unique block.

- **Excel Integration:**  
  Attendance data is appended to an Excel file using `openpyxl`. The program checks for an existing session block at the top of the file and updates it if necessary, while older blocks remain intact.

- **Sound Notifications:**  
  The built-in `winsound` module is used to play different beep sounds corresponding to different events (Time In, Time Out, error).

## Customization

- **Newline in Excel Cells:**  
  To include newlines in Excel cells, use the newline character (`\n`) and enable text wrapping with openpyxl’s `Alignment`.

- **File Paths:**  
  You can change the Excel file save path by modifying the `folder_path` variable in the `save_to_excel()` method.

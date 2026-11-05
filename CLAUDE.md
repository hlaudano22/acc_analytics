# Accounting Analytics (tweaks on top of the OneDrive CLAUDE.md)
- This file wins over the OneDrive one when they conflict.

# Folders
- `Classwork\`: in-class starter notebooks and Alteryx work. The whole course folder is one git repo.
- `Assignments\`: HW and project folders.
- `Data_Files\`: all data files (xlsx, csv, yxdb). Notebooks go in Classwork or Assignments, not here.
- `Lecture_Notes\`: slides and notes.
- `Lecture_Notes\Transcripts\`: class transcripts I had auto-generated from Kaltura, named `M.D Topic.txt`.
- When I say "grab my downloads", notebooks go to `Classwork\` and data files go to `Data_Files\`. Skip files that are exact copies of ones already there.

# Use the class files for context
- For labs and assignments, read the transcripts, slides and my earlier labs yourself before answering or checking my work. I prefer that over you asking me or guessing what was said in class. Cite timestamps when you use a transcript.
- If the transcript for a class isn't there yet, use the `uva-canvas` skill to make it.
- Transcripts are auto-generated and mishear terms ("AUI" for ROE, "crisp" for CRSP). Student help conversations are garbled. If something on-screen matters, check the video.

# Code style
- For Python here, match this class's starter notebooks, not the COMM 4259 labs.
- Alteryx is the main tool for this class. If I ask how to do something, assume Alteryx unless I say Python.

# Submitting Python labs
- Export to HTML next to the notebook, named `<notebook name>_HenryLaudano.html`.

# Loading data in Python labs
- The lab code reads files by name only, but my data is in `Data_Files\`, not next to the notebook. So I use a `load_data` function instead.
- When I say "add the define function for loading data" (or similar) in a new notebook, replace the lab's `read_excel` line in the "bring in data" step with this cell. Keep the lab's variable names (e.g. `comp1`) and file names (often `-1` from the download):

```python
# function so i only type the file name (works on both computers) [I made cause I don't keep stuff in same folder]
def load_data(file_name, rows=5):
    # check the end of the file name to pick the right reader
    if file_name.endswith('.csv'):
        reader = pd.read_csv
    else:
        reader = pd.read_excel
    # try personal computer path first, then school desktop
    try:
        df = reader('C:\\Users\\Henry\\OneDrive - University of Virginia\\COMM Semester 3\\1. Accounting Analytics\\Data_Files\\' + file_name, index_col=False)
    except FileNotFoundError:
        df = reader('C:\\Users\\fbw4vt\\OneDrive - University of Virginia\\COMM Semester 3\\1. Accounting Analytics\\Data_Files\\' + file_name, index_col=False)
    # show the first rows (5 unless i give a different number)
    display(df.head(rows))
    return df

comp1 = load_data('file_name-1.xlsx')
```
- It picks the reader from the file ending: `.csv` uses `read_csv`, anything else (xlsx) uses `read_excel`.
- For exporting a file, HW5 has a matching `save_data` function that saves to `Data_Files\`. It catches `OSError`, because `to_csv` doesn't raise `FileNotFoundError` when the folder is missing.

# Live notebook edits in VS Code
- If the session starts with `ide` failed to connect (`CONNECTION_CLOSED`), tell me right away. Notebook edits still save to disk but may not show live in my window.
- Running `/ide` didn't fix this on 11/4/2026. Restarting the Claude Code chat did. Restarting stops background agents, so check for running ones first and resume them after.

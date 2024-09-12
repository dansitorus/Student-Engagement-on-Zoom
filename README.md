## Student-Engagement-on-Zoom
# Project Overview
In the realm of online education, student engagement is essential, especially as universities increasingly rely on virtual platforms like Zoom for instruction. To gauge and boost student involvement, many courses integrate a class participation score into the overall assessment. However, quantifying each student's engagement through their virtual interactions presents challenges.
This project seeks to tackle these challenges by leveraging auto-generated transcripts from Zoom sessions to determine each student's total speaking duration during class. By quantifying airtime in milliseconds, this study aims to provide a measurable indicator of student participation. This data will offer valuable insights to help educators refine engagement strategies and enhance the online

# Data
The Zoom auto-generated transcript is formatted in VTT (Web Video Text Tracks). Each entry in the transcript spans three lines and is separated from the next by a blank line. The structure of each entry is outlined below:
Sequence Number (SNo): Identifies the order of entries
Time Range: [TimeFrom] --> [TimeTo] indicates the duration of the utterance
Speaker and Utterance: [RegName]: [Utterance] shows the registered name of the speaker followed by their spoken words

![Screenshot 2024-09-13 021853](https://github.com/user-attachments/assets/c0db0ddb-33d1-452e-88e8-c788751ec508)

# Setting Up the Python Environment for VTT Data Processing
To effectively process the VTT files from Zoom auto-generated transcripts, essential Python libraries are initially imported. The library re (Regular Expressions) is particularly crucial for text processing, allowing for pattern matching and the extraction of specific data formats, essential for parsing the VTT transcript files.

Steps to Process VTT Files:
Import Libraries: Import necessary Python libraries including re for regular expressions
Define Variables: Set up variables to capture key elements from the VTT files, such as timestamps and speaker names
Regex Patterns: Establish regex patterns to identify and extract relevant data from the transcript text
Line-by-Line Processing:
Iterate through each line of the VTT file, matching it against predefined regex patterns
Extract and store relevant information in variables based on these matches
Use an elif loop to manage scenarios where entries might be missing speaker information or contain simultaneous speakers

![Screenshot 2024-09-13 022635](https://github.com/user-attachments/assets/280cdad7-3014-4445-93f3-c55bd84a922d)

Data Structuring:
Organize the extracted data into a structured table format, ready for further analysis
Database Connection:
Utilize sqlalchemy to create a connection between Python and a MySQL database
Employ the to_sql method to write the structured DataFrame to a new table in the database

![Screenshot 2024-09-13 022807](https://github.com/user-attachments/assets/d2b68a33-bede-4dba-be2e-f1616cb1138d)

# SQL Data Preparation for Student Engagement Analysis
To facilitate the evaluation of student engagement data, the original vtt table was cloned into a new table called vttclean. The data types of the timefrom and timeto columns were refined to TIME(3) to accurately capture time in milliseconds. Following this adjustment, the duration between timefrom and timeto for each record was computed, with the results converted from microseconds to milliseconds. This calculated duration was then stored in a newly added column within the vttclean table. These modifications provided a precise and well-prepared dataset, setting a robust groundwork for subsequent analysis of student participation.

# Data Visualization for Student Engagement Using R
R was chosen for this analysis due to its powerful data manipulation and visualization capabilities. Libraries such as RMySQL, dplyr, forcats, and ggplot2 were utilized to facilitate a seamless connection to the MySQL database, process the data, and generate effective visual representations.

The process began with establishing a connection to the anl503 database and importing the vttclean table into a data frame. The next step involved calculating the total speaking time for each student by aggregating the milliseconds column. Entries where the RegName was 'INSTRUCTOR' or absent were excluded to focus on student data.

To enhance readability, the data was organized in descending order of total airtime using the fct_reorder function from the forcats package. The final visualization was crafted using ggplot2, producing a bar chart that distinctly showcases the accumulated speaking time for each student. This visual aid effectively highlights differences in student engagement levels, allowing for easy comparison and analysis.

![Screenshot 2024-09-13 023027](https://github.com/user-attachments/assets/ee48ccde-2a9f-4716-a61a-47290d8971e6)











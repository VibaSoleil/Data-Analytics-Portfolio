Data Analyst Automation Project Troubleshooting Notes
Python Environment Issue

Problem:

The Python version encountered issues at one point.
There was a difference between the installed Python version and the one being used.

Solution:

Check the Python version.
Use a stable Python version.
Ensure that the libraries are available:
pandas
numpy
fastapi

Docker Issue

Problem:

The Python Docker container was unstable.
The container would start and then stop by itself.
There were issues when running the environment.

Solution:

Check the container status.
Check the Docker logs.
Ensure that the image and container are running correctly.
Understand the relationship:
Docker → runs the environment
Python API → runs the analysis process

Python API Issue

Problem:

The HTTP Request from n8n generated:
Internal Server Error 500
The API did not process the request correctly.

Solution:

Check the FastAPI code.
Ensure that the endpoint is correct.
Ensure that the JSON request format is correct.
Ensure that the file path can be read by the container.

File Path Issue

Problem:

Python could not find the CSV file.
There was a difference between the file location on the computer and in Docker.

Solution:

Check the folder location.
Adjust the file path.
Understand the difference between:
Windows path
path inside the Docker container

n8n Workflow Issue

Problem:

Difficulty organizing the order of the nodes.
Incorrectly connecting the nodes.
The HTTP Request node did not receive the correct input.

Solution:
Create a simple flow:

Read/Write File
↓
HTTP Request Cleaning
↓
HTTP Request Analysis
↓
Save Output

Result Validation Issue

Problem:

Concern that the automation results might differ from the manual process.

Solution:

Use Manual Python as the reference.
Compare:
number of rows
number of columns
cleaning results
analysis results

Troubleshooting Principles Applied

When an error occurs:

Do not immediately change multiple things.
Check one part at a time:
data
code
API
Docker
n8n
Compare the results with a known output.



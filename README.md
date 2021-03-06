# Test for Analytics

Design tests for Analytics functionality on a Battery Monitoring System.



## Analysis-functionality to be tested

This section lists the Analysis for which _tests_ must be written.

Battery Telemetrics are collected and stored on a server.
Data for a month is stored in a [csv file](https://en.wikipedia.org/wiki/Comma-separated_values).

Analysis must be done on this csv file to find the following:
- minimum
- maximum
- count of breaches (how many times did it cross the threshold in a month?)
- record trends (date & time when the reading was continuously increasing for 30 minutes)

A PDF report of the analysis must be stored every week.
Notification must be sent when a new report is available.

## Tasks

### List Dependencies

List the dependencies of the Analysis-functionality.

1. Credentials info and Access to the Server containing the telemetrics in a csv file.
2. Read Access to the Battery telemetrics data in a csv file.
3. Information to understand valid and invalid inputs in csv file
4. Information regarding the breach threshold of Battery telemetrics.
5. Access of Date and Time Stamp information to record trends.
6. Third party Tools/ Libraries for the PDF generation.
7. Credentials info and Access to the server to store the PDF reports generated weekly.
8. Access to the notification medium.(Email receipents or Controller or Console)
9. Tools/Scripts to perform unit testing.


(add more if needed)

### Mark the System Boundary

What is included in the software unit-test? What is not? Fill this table.

| Item                      | Included?     | Reasoning / Assumption
|---------------------------|---------------|---
Battery Data-accuracy       | No            | We do not test the accuracy of data
Computation of maximum      | Yes           | This is part of the software being developed
Off-the-shelf PDF converter | No            | Tools/Libraries can be used for PDF conversion. Only PDF generation invocation can be checked via PDF generation Function call,but actual PDF conversion is not part of our test
Counting the breaches       | Yes           | Total Occurance of number of breaches in a month is a part of the software being developed
Detecting trends            | Yes           | Date & Time when the reading was continuously increasing for 30 minutes is recorded as part of the software being developed      
Notification utility        | No            | Notification is triggered and Status of Notification sent to any medium can be tested as a mock function(incase of Failure in notification sent), but actual notification mechanism is not tested

### List the Test Cases

Write tests in the form of `<expected output or action>` from `<input>` / when `<event>`

Add to these tests:

1. Write minimum and maximum to the PDF from a csv containing positive and negative readings
2. Write "Invalid input" to the PDF when the csv doesn't contain expected data
3. Write "no data" to the PDF when the csv file is empty.
4. Write "wrong format of input file" when the server contains any other file format other than csv file.
5. Write total number of breaches occured in a month.
6. Write "0" when there are no breaches recorded in a month.
7. Write the recorded trend (Date & time when the reading was continuously increasing for 30 minutes)
8. Check whether Date and time stamp is insync with Real Time System.
9. Generate PDF report from csv file every week with a return status as "pdf successfully generated".
10. Notify the notification medium when new PDF report is available with return status as " Notification sent succesfully"
11. Return status "Pdf generation Failure" if the PDF generation is missing for any week
12. Return status "Notification Failure" if the notification is not sent when the pdf is generated/ when the notification is not sent on weekly basis.
13. Check if the Notification is sent to all recipients/medium defined.
14. Check for inaccessible Server behaviour when the Server containing csv or Pdf is not accessible.
15. Check for data format (minimum, maximum,breach count, trend columns) inside the csv file and return "invalid data format" if the format is incorrect.


(add more)

### Recognize Fakes and Reality

Consider the tests for each functionality below.
In those tests, identify inputs and outputs.
Enter one part that's real and another part that's faked/mocked.

| Functionality            | Input         | Output                      | Faked/mocked part
|--------------------------|-------------- |-----------------------------|---
Read input from server     | csv file      | internal data-structure     | Fake the server store
Validate input             | csv data      | valid / invalid             | None - it's a pure function
Notify report availability | pdf report    | mail notification           | Mock the mail notification invocation with Fn call status
Report inaccessible server |Server address | csv or pdf                  | mock server availability
Find minimum and maximum   | csv data      | minimum and maximum values              | None - it's a pure function
Detect trend               | csv data     |recorded trend with date and time stamp             | None - it's a pure function
Write to PDF               | analysed csv file      | PDF report with min, max, breach count and trend data                 | Mock the PDF conversion invocation with Fn call status

# Jenkins: Build Triggers 

### We all know that Jenkins is a well-known open-source continuous integration and continuous deployment automation tool

### These are the most common Jenkins build triggers:
1. Trigger builds remotely
2. Build after other projects are built
3. Build periodically
4. GitHub hook trigger for GITScm polling
5. Poll SCM

## 1. Trigger builds remotely :
If you have any desire to set off your venture worked from anyplace whenever then you ought to choose Trigger forms remotely choice from the form triggers.

You'll have to give an approval token as a string so just the individuals who realize it would have the option to set off this undertaking's fabricates from a distance. This gives the predefined URL to remotely summon this trigger.

```sh
    predefined URL to trigger build remotely: 

    JENKINS_URL/job/JobName/build?token=TOKEN_NAME

    JENKINS_URL: the IP and PORT which the Jenkins server is running
    TOKEN_NAME: You have provided while selecting this build trigger.
```    
Whenever you will hit this URL from anywhere you project build will start.

## 2. Build after other projects are built
On the off chance that your venture relies upon another task fabricate, you ought to choose Build after different undertakings are constructed choice from the form triggers.

In this, you should determine the project(Job) names in the Projects to watch field segment and select one of the accompanying choices:
  - Trigger only if the build is stable
  - Trigger even if the build is unstable  
  - Trigger even if the build fails

After that, It starts watching the specified projects in the Projects to watch section.

## 3. Build periodically:
If you want to schedule your project build periodically then you should select the Build periodically option from the build triggers.

syntax of cron (with minor differences). Specifically, each line consists of 5 fields separated by TAB or whitespace:
```sh
  MINUTE HOUR DOM MONTH DOW
```
```sh
  MINUTE	Minutes within the hour (0–59)
  HOUR	The hour of the day (0–23)
  DOM	    The day of the month (1–31)
  MONTH	  The month (1–12)
  DOW	    The day of the week (0–7) where 0 and 7 are Sunday.
```  
To specify multiple values for one field, the following operators are available. In the order of precedence,
- * specifies all valid values
- M-N specifies a range of values
- M-N/X or */X steps by intervals of X through the specified range or whole valid range
- A,B,...,Z enumerates multiple values

### Examples:
```sh 
  # Every fifteen minutes (perhaps at :07, :22, :37, :52):
  H/15 * * * *
  # Every ten minutes in the first half of every hour (three times, perhaps at :04, :14, :24):
  H(0-29)/10 * * * *
  # Once every two hours at 45 minutes past the hour starting at 9:45 AM and finishing at 3:45 PM every weekday:
  45 9-16/2 * * 1-5
  # Once in every two hour slot between 8 AM and 4 PM every weekday (perhaps at 9:38 AM, 11:38 AM, 1:38 PM, 3:38 PM):
  H H(8-15)/2 * * 1-5
  # Once a day on the 1st and 15th of every month except December:
  H H 1,15 1-11 *
```
After successfully scheduled the project build then the scheduler will invoke the build periodically according to your specified duration.

## Time zone specification
Periodic tasks are normally executed at the scheduled time in the time zone of the Jenkins master JVM (currently UTC). This behavior can optionally be changed by specifying an alternative time zone in the first line of the field. Time zone specification starts with TZ=, followed by the ID of a time zone.
Complete example of a schedule with a time zone specification:
```sh
   TZ=Asia/Kolkata
    # This job needs to be run in the morning, London time
    H 8 * * *
    # Butlers do not have a five o'clock, so we run the job again
    H(0-30) 17 * * *
```    

## 4. GitHub webhook trigger for GITScm polling:

A webhook is an HTTP callback, an HTTP POST that occurs when something happens through a simple event-notification via HTTP POST.

GitHub webhooks in Jenkins are used to trigger the build whenever a developer commits something to the branch.

Let’s see how to add build a webhook in GitHub and then add this webhook in Jenkins.

  1. Go to your project repository.
  2. Go to “settings” in the right corner.
  3. Click on “webhooks.”
  4. Click “Add webhooks.”
  5. Write the Payload URL as 

```sh
  https://example.com/postreceive
  //This URL is a example URL where the Jenkins server is running
```

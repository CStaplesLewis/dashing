![Jenkins Build Status History - screenshot](http://i.imgur.com/Ty8PTjY.png "Jenkins build status history - screenshot")

Description
===========
The **Jenkins Build Status History** widget periodically fetches a snapshot of build status information for a specified list of jobs on a Jenkins CI server.

As time progresses, new build status samples are added to the right, while older samples are removed from the left. This view allows you to quickly see the health of your jobs as well as any time trends.

Calls are made to the [Jenkins API](https://wiki.jenkins-ci.org/display/JENKINS/Remote+access+API) to retrieve the __name__ and __color__ properties of listed jobs in a JSON form. The __color__ of a given job represents its current build status 
(i.e. __"blue"__ => __successful build__, __"red"__ => __failing build__ and so on).

The build colours are rendered within the widget using the [Raphaël JavaScript library](http://raphaeljs.com/) for vector graphics.

This widget borrows some code from the [Rickshaw widget](https://gist.github.com/jwalton/6614023).

## Installing the widget

#### Raphaël
You need the Raphaël library to use the widget. Get the latest version [here](http://raphaeljs.com/).

Place __`raphael.min.js`__ in your __`assets/javascripts`__ folder

#### Widget files

Place the following files in a folder called `widgets/buildhistory`:  
  - __`buildhistory.coffee`__
  - __`buildhistory.html`__
  - __`buildhistory.scss`__

#### Build history retrieval job
Place the following file in your `jobs/` folder:
  - __`buildhistory.rb`__

## Adding the Jenkins Last Commit widget to your dashboard
To add this widget to your dashboard, add the following to your __`<Dashboard-filename>.erb`__ file:
```HTML
    <li data-row="1" data-col="1" data-sizex="1" data-sizey="1">
        <div data-id="buildhistory" data-view="Buildhistory" data-max_samples="100" data-show_job_titles="true" data-sample_spacers="true"></div>
    </li>
```

Notice that the widget has a few parameters:

|Parameter|Meaning | 
|:------------- |:------------------|
| `data-max_samples` | Number of build status samples to store before discarding old values  | 
| `data-show_job_titles` |  **true** if job titles must be rendered on widget, **false** if no titles to be rendered |
| `data-sample_spacers` | If true then a single space is inserted between samples & rows. |

## Configuring the widget for use with your Jenkins instance
There are a few parameters that must be set up before using this widget with your Jenkins instance.

In the __`buildhistory.rb`__ file, modify the following parameters according to your needs:

|Parameter|Meaning | 
|:------------- |:------------------|
| `JENKINS_BUILD_STATUS_HISTORY_URI` | Jenkins base URL  | 
| `$jenkins_jobs_to_be_tracked` | This is an array containing job names to be tracked on Jenkins|
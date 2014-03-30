# Sprinter

<table>
<tr>
  <td>
    <img src="http://maxcdn.fooyoh.com/files/attach/images/591/736/904/004/haters_gonna_hate.gif"/>
  </td>
  <td>
    <p/>Provides some extended utilities for the Github API for operating against multiple Github issue trackers at once.
  </td>
</tr>
</table>

If you're like me, this library might save you an hour a week. I'm a "scrum master", which sounds silly but is actually a real thing. <a href="https://github.com/numenta/">We have a lot of repos on Github</a>. Most of them have issue trackers. So it takes a long time to update all of them for common recurring tasks like sprint changes. This library takes your Github credentials [2] and gives you easy ways to set up tasks that execute against multiple Github Issue Trackers at once, so you can:

Run the following actions across multiple repos:

- list issues 
- list milestones
- create milestones 
- close  milestones 


[1] There is no [1].

[2] Should I be using a different authentication method? If so, [please file a bug](https://github.com/rhyolight/sprinter.js/issues). 

## Installation

### As a library for local scripts

    npm install sprinter

Now you can `require('sprinter')` and use as defined below in the [examples](#examples).

### As a command line tool

    npm install -g sprinter

Now you can run `sprinter` from the command line. 

    sprinter --help

Displays usage information. 

## Examples

### Creating the Client

    var Sprinter = require('sprinter');

    var sprinter = new Sprinter(
        <username>,
        <password>,
        ['org1/repo1', 'org1/repo2', 'org2/repo1']
    );

### Listing All Issues Across All Repos

    sprinter.getIssues(function(err, issues) {
        console.log(issues);
    });

### Listing All Milestones Across All Repos

Milestones will be grouped by title.

    sprinter.getMilestones(function(err, milestones) {
        console.log(milestones);
    });

### Creating A Milestone Across All Repos

    sprinter.createMilestones({
        title: 'Sprint 20',
        due_on: 'Apr 16, 2014'
    }, function(err, milestones) {
        console.log(milestones);
    });

### Closing Milestones by Title Across All Repos

Closes all milestones with the title `Sprint 18` across all monitored repos.

    sprinter.closeMilestones('Sprint 18', function(err, closed) {
        console.log('Closed milestones:');
        console.log(closed);
    });

# Rails Girls Attendees

This little generater is for showing off all the organizers, coaches and attendees of the Rails Girls Switzerland movement.

* [Basel, April 2013](http://railsgirlsswitzerland.github.io/attendees/site/2013_04_basel.html)

## How to setup a new event

* Add the event to events.yml
* Add a new directory in the events directory - make sure the directory name is the same one you defined in events.yml  
  Make sure the directory name is following this naming structure: `YYYY-MM-locationname`, e.g. `2013-04-basel`
* Add two files to the new event directory: `organizers.yml` and `attendees.yml`
* Add all the people to the lists. An entry has the attributes:
  - `name`
  - `email`
  - `twitter` - takes only the twitter handle like this: `@danielpuglisi`
  - `avatar` - takes an url for an image, if left blank it is going to look for a gravatar image based on the given `email` address
* Run `rake generate` on the command line to generate the html version of the lists

## Publish a new event

* run `rake publish`

## Todo

* Merge this into a real rails app!

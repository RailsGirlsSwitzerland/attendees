require 'yaml'
require 'digest'

def generate_gravatar_hash(email)
  Digest::MD5.hexdigest(email.strip.downcase) if email
end

def generate_html_entry(person)
  output =  "\t<li class='left'>\n"
  output += "\t\t<span class='avatar'><img src='http://www.gravatar.com/avatar/#{generate_gravatar_hash(person['email'])}?d=identicon' class='round left'></span>\n"
  output += "\t\t<span class='name'>#{person['name']}</span>\n"
  output += "\t\t<span class='twitter'><a href='http://twitter.com/#{person['twitter']}'><i class='icon-twitter'></i></a></span>\n" if person['twitter']
  output += "\t\t<span class='email'><a href='mailto:#{person['email']}'><i class='icon-envelope-alt'></i></a></span>\n" if person['email']
  output += "\t</li>\n"
end

def generate_html_list(people)
  output = "<ul>\n"
  people.each do |person|
    output += generate_html_entry(person)
  end
  output += "</ul>\n"
  output += "<div class='clear'></div>\n"
end

task :generate do
  events = YAML.load_file("events.yml")

  events.each do |event|
    directory  = event["directory"]
    organizers = YAML.load_file("events/#{directory}/organizers.yml")
    attendees  = YAML.load_file("events/#{directory}/attendees.yml")

    File.open("site/#{directory}.html", "w") do |file|

      output = "<h1>Organizer & Coaches</h1>\n"
      output += generate_html_list(organizers)

      output += "<h1>Attendees</h1>\n"
      output += generate_html_list(attendees)

      file.write <<-END.gsub(/^ {8}/, '')
        <!doctype>
        <html>
        <head>
          <title>#{event['name']} attendees</title>
          <link rel='stylesheet' href='stylesheets/application.css'>
        </head>
        <body>
        <div class="header">
          <div class="wrapper">
            <div class="inner">
              <div class="left">
                The people who attended #{event['name']} - #{event['date']}
              </div>
              <div class="right">
                <a href="http://en.gravatar.com/">Add your avatar</a>
              </div>
              <div class="clear"></div>
            </div>
          </div>
        </div>
        <div class="main">
          <div class="wrapper">
            <div class="inner">
        #{output}
            </div>
          </div>
        </div>
        <div class="footer">
          <div class="wrapper">
            <div class="inner">
              <a href='https://github.com/RailsGirlsSwitzerland/attendees'>Fork me on <i class="icon-github"></i></a>
            </div>
          </div>
        </div>
        </body>
        </html>
      END

    end

    system('compass compile')
  end
end

# Publishes the content under site to gh-pages branch - you probably need to run `rake generate` first
task :publish do
  `git checkout gh-pages`
  `git checkout master -- site`
  `git add .`
  `git commit -am "generated pages"`
  `git push origin gh-pages`
  `git checkout master`
end

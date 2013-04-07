require 'yaml'

def generate_html_entry(person)
  output =  "\t<li>\n"
  output += "\t\t<span class='name'>#{person['name']}</span>\n"
  output += "\t\t<span class='twitter'>#{person['twitter']}</span>\n" if person['twitter']
  output += "\t\t<span class='email'>#{person['email']}</span>\n" if person['email']
  output += "\t</li>\n"
end

def generate_html_list(people)
  output = "<ul>\n"
  people.each do |person|
    output += generate_html_entry(person)
  end
  output += "</ul>\n"
end

task :generate do
  events = YAML.load_file("events.yml")

  events.each do |event|
    directory  = event["directory"]
    organizers = YAML.load_file("events/#{directory}/organizers.yml")
    attendees  = YAML.load_file("events/#{directory}/attendees.yml")

    system("mkdir -p site/#{directory}")

    File.open("site/#{directory}/index.html", "w") do |file|

      output = "<h1>Organizer & Coaches</h1>\n"
      output += generate_html_list(organizers)

      output += "<h1>Attendees</h1>\n"
      output += generate_html_list(attendees)

      file.write <<-END.gsub(/^ {8}/, '')
        <!doctype>
        <html>
        <head>
          <title>#{event['name']} attendees</title>
          <link ref='stylesheet' src=''>
        </head>
        <body>
        <div class="header">
          <div class="wrapper">
            <div class="inner">
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
        </body>
        </html>
      END

    end
  end
end

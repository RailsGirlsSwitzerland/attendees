require 'yaml'

def generate_html_entry(person)
  output =  "<li>\n"
  output += "<span class='name'>#{person['name']}</span>\n"
  output += "<span class='twitter'>#{person['twitter']}</span>\n" if person['twitter']
  output += "<span class='email'>#{person['email']}</span>\n" if person['email']
  output += "</li>\n"
end

task :generate do
  events = YAML.load_file("events.yml")

  events.each do |event|
    directory  = event["directory"]
    organizers = YAML.load_file("events/#{directory}/organizers.yml")
    attendees  = YAML.load_file("events/#{directory}/attendees.yml")
    system("mkdir -p site/#{directory}")
    File.open("site/#{directory}/index.html", "w") do |file|
      organizers.each do |organizer|
        file.write generate_html_entry(organizer)
      end
    end
  end
end

require 'rake'
require 'net/http'

task :trigger_build, [:token, :projects] do |t, args|
  args[:projects].split(' ').each do |project|
    uri = URI.parse("https://api.shippable.com/projects/#{project}/build?token=#{args[:token]}")
    http = Net::HTTP.new(uri.host, uri.port)
    http.use_ssl = true
    response = http.request(Net::HTTP::Post.new(uri.request_uri))
    code = response.code.to_i
    if code < 200 and code >= 300
      puts response.body
      exit 1
    end
  end
end

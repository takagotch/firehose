### firehose
---
https://github.com/firehoseio/firehose

```
gem install firehose
firehose server
curl "http://localhost:7474/hello"
curl -X PUT -d "Greetings fellow human being..." "http://localhost:7474/hello"

curl -x PUT -d "\"This is almost magical\"" "http://localhost:7474/hello"
firehose javascript > firehose.js
```

```ruby
new Firehose.Consumer(
  message: funciton(msg){
    console.log(msg);
  },
  connected: function(){
    console.log("Well shuncks, we're not connected anymore");
  },
  disconnected: function(){
    console.log("Well shuncks, we're not connected anymore");
  },
  error: function(){
    console.log("Well then, something went horribuly wrong.");
  },
  uri: '//localhost.7474/hello'
).connect();

new Firebose.MultiplexedConsumer({
  connected: function(){
    console.log("Great Scotts!! We're connected!");
  },
  disconnected: function(){
    console.log("Well shucks, we're not connected anymore");
  },
  error: function(){
    console.log("Well then, something went horribly wrong.");
  },
  uri: '/localhost:7474/',
  channels: {
    "/my/channel/1": {
      last_sequence: 10,
      message: function(msg){
        console.log("got message on channel 1:"
        console.log(msg);
    }
  },
  "/my/channel/2": {
    message: function(msg) {
      console.log("got message on channel 2:");
      console.log(msg);
    }
  }
}).connect();

require 'firehose'
require 'json'
json = {'hello' => 'world'}.to_json
firehose = Firehose::Client::Producer::Http.new('//127.0.0.1:7474')
firehose.publish(json).to("/my/messages/path")

firehose = Firehose::Client::Producer::Http.new('//127.0.0.1:7474')
firehose.publish(json).to("/my/messages/path", deprecated: true)
firehose.publish(json).to("/my/messages/path", ttl: 120)
firehose.publish(json).to("/my/messages/path", buffer_size: 1)
firehose.publish(json).to("/my/messages/path", persist: true)

require "firehose"
class MyFilter < Firehose::Server::MessageFilter
  def process(message)
    name = params["name"]
    message.payload = "HEY #{name}!, #{message.payload.upcase}!"
  end
end
Firehose::Server.configuration do |config|
 config.message_filter = MyFilter
 config.redis.url = ENV.fetch "FIREHOSE_REDIS_URL", "redis://redis:6379/10"
end

class MyFilter < Firehose::Server::MessageFilter
  def initialize(channel)
    super(channel)
    MyLogger.info "Subscribing to channel: #{channel}"
  end
  def on_subscribe(params)
    @my_param = params["my-param"].to_i
    # { error: "Subscription failed", reason: error_reason }
  end
  def process(message)
    if @my_params > 10
      message.payload += "My-Param: #{@my_param}"
    end
  end
  def on_unsubsribe
  end
end

firehose = Firehose::Client::Producer::Http.new('//127.0.0.1:7474')
firehose.publish("{'hello': 'world'}").to("/my/messages/path", deprecated: true)

Firehose::Server.configuration do |config|
  config.deprecated_channels = ["/foo/bar.json", "/foo/bar/baz.json"]
  config.deprecated_channel do |channel|
    channel =~ /^/foo\/*\.json$/
  end
end

require 'firehose'
consumer = Firehose::Rack::Consumer.new do |app|
  app.http_long_poll.timeout = 20
end

require 'firehose'
run Firehose::Rack::Publisher.new

my_sprockets_env = Sprockets::Environment.new
Firehose::Assets::Sprockets.configure my_sprockets_env

if exceptional_key = ENV['EXCEPTIONAL_KEY']
  require 'exceptional'
  EM.error_handler do |e|
    Firehose.logger.error "Unhandled exception: #{e.class} #{e.message}\n#{e.backtrace.join "\n"}"
    ::Exceptional.handler(e)
  end
end

gem "firehose"
gem "airbake"
gem "rainbows", :require => false
gem "rack", "1.4.0"
gem "foreman", :require => false
gem "capistrano", :require => false
```

```js
#= require some/other/js/file
#= require lib/firehose_config
#= requrie firehose
#= require some/more/js/files
```



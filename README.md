# Rack::Plastic

## Description

If you are creating Rack middleware that changes the HTML response, use
Rack::Plastic to get a head start.  Rack::Plastic takes care of the
boilerplate Rack glue so that you can focus on simply changing the HTML.

## Usage

There are two ways you can change the HTML: as a Nokogiri document or as
a string.  Simply define one of the following methods:

    def change_nokogiri_doc(doc)
      ... insert code that changes the doc ...
      doc
    end

    def change_html_string(html)
      ... insert code that changes the html string ...
      html
    end

If you define both methods, change_nokogiri_doc will be called first, then
the doc will be converted to an HTML string, then the string will be
passed to change_html_string.

Rack::Plastic also provides some convenience methods for interacting with
Rack and Nokogiri as well as some convenience methods for testing.

## Examples

The examples/middlewares directory has examples of writing middleware using
Rack::Plastic.

## Rails Streaming

This middleware is not compatible with Rails HTTP streaming.  According to [Railscast #266](http://asciicasts.com/episodes/266-http-streaming):
"Also, streaming is incompatible with some middleware. If the middleware modifies the response
then it will not work with streaming."

## Testing

Rack::Plastic comes with some test helpers that make it easier for you to
write tests for your Rack middleware.  Refer to the documentation for
PlasticTestHelper for more details.

If you want to test Rack::Plastic itself, this gem doesn't come with automated tests,
but it provides manual tests.  Each of the example middlewares is inserted into a
Sinatra, Rails, and Rack test app.

To run the Rails test app:

* cd examples/railsapp
* script/server
* point your browser to http://localhost:3000

To run the Sinatra test app:

* cd examples/sinatraapp
* ruby app.rb
* point your browser to http://localhost:4567

To run the Rack test app:

* cd examples/rackapp
* rackup config.ru
* point your browser to http://localhost:9292

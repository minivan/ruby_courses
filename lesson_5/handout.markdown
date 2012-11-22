
##Sinatra:

    $ gem install sinatra

#Hello World!

    require 'rubygems' if RUBY_VERSION < '1.9'
    require 'sinatra';

    get '/' do
      'Minimal Sinatra Hello World!'
    end

Now, open a Terminal window and type:

    ruby minimal.rb

Finally, go to this address: `http://127.0.0.1:4567/`

To stop the program, go to the Terminal window and press `Ctrl+C`

#Adding Structure: `Sinatra::Base`

It’s useful to structure the program as a class.

    require 'sinatra/base'

    class MyApp < Sinatra::Base
      get '/' do
        'Hello World!'
      end
    end

    MyApp.run!

now `ruby myapp_base.rb`

#Structure: A Separate App File

Create two files:

Application - `my_app.rb`

    require 'sinatra/base'

    class MyApp < Sinatra::Base
      get '/' do
        'Hello World from MyApp in separate file!'
      end
    end

Launcher - `run_my_app.rb`

    require 'my_app'

    MyApp.run!

They have to be in the same directory!
Now run them:
    ruby run_my_app.rb

# Static Files

A Web application will often have dynamic content (what we’ve created so far) and static content (e.g. images).

Create a directory ‘static’, and create a file called `index.html` containing:

**This is a static file.**

Static Files - my_app.rb

    require 'sinatra/base'

    class MyApp < Sinatra::Base
      set :static, true
      set :public, File.dirname(__FILE__) + '/static'
    end

# extra: Some Routes

Create a file `static/routes.html` with the content:

    <ul>
      <li><a href="named_via_params/foo">Named parameters via params Hash</a></li>
      <li><a href="named_via_block_parameter/foo">Named parameters via block parameters</a></li>
      <li><a href="splat/foo/bar/baz">Multiple parameters via params[:splat]</a></li>
      <li><a href="splat_extension/myfile.txt">Filename via params[:splat]</a></li>
      <li><a href="regexp_params_captures/foobar">Using regular expression via params[:captures]</a></li>
      <li><a href="regexp_captures_via_block_parameter/foobar">Using regular expression via block parameters</a></li>
    </ul>

Now in the script you have a whole bunch of options for routing:

    require 'sinatra/base'

    class MyApp < Sinatra::Base
      set :static, true
      set :public, File.dirname(__FILE__) + '/public'

      get '/named_via_params/:argument' do
        "
        Using: '/named_via_params/:argument'<br/>
        params[:argument] -> #{params[:argument]} (Try changing it)
        "
      end

      get '/named_via_block_parameter/:argument' do |argument|
        "
        Using: '/named_via_block_parameter/:argument'<br/>
        argument -> #{argument}
        "
      end

      get '/splat/*/bar/*' do
        "
        Using: '/splat/*/bar/*'<br/>
        params[:splat] -> #{params[:splat].join(', ')}
        "
      end

      get '/splat_extension/*.*' do
        "
        Using: '/splat_extension/*.*'<br/>
        filename -> #{params[:splat][0]}<br/>
        extension -> #{params[:splat][1]}
        "
      end

      get %r{/regexp_params_captures/([\w]+)} do
        "params[:captures].first -> '#{params[:captures].first}'"
      end

      get %r{/regexp_captures_via_block_parameter/([\w]+)} do |c|
        "c -> '#{c}'"
      end

    end

    Go to `http://127.0.0.1:4567/routes.html`

You will see a list of links which exemplify different types of route matching.

# Templates

Create a `views` directory.

The template - `views/index.erb`

    This is <%= @foo %>
    Templates - templates.rb

Now in the script file:

    require 'sinatra/base'
    require 'erb'

    class MyApp < Sinatra::Base
      get '/template' do
        @foo = 'erb'
        erb :index
      end
    end

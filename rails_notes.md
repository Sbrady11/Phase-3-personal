inside the terminal
`$ rails new suggestion-box -T -d=postgresql`

  (would generate a new rails app)
  options to add, -T

`$ cd suggestion-box`

looking at the app folder within the application
  assets --> all this sent through the pipeline
      config
      images
      javascript
      stylesheet
  channels
    application_cable --> do a talk perhaps? listening for web sockets, complex!
      channel.rb
      connection.rb
  controllers --> responsible for managing the operation flow of  -your app

  helpers --> used for views stuff (should be light in our apps)
          --> formatting stuff
          --> conversions, etc..
  jobs --> bacgkrounds, sit outside the response/get cycle, does -stuff

  models --> resources, objects, the universe of the app! hold the max amount of logic and functionality

  views
    layouts --> auto links your css and javascript
  bootstrap files shouldnt be wtih the assets/javascript folder
bin
  --> wont be touched
config
  --> may mess with this, but not too likely
  routes.rb
      --> You'll live here!
db
  seeds.rb
  will have migrations too
lib
  code that you wrote, but not necessary for the core function
log
  rails is notoriously verbose
    saved to the log
temp
  --> not touched, intermediation files for the interum process
----------------------------------------------------------------------------
step 1. --> teamtreehouse lecture on bin/rails
  create a database
  rails console
    rails c
    rails s --> server
  still need rake db:drop, create, migrate 

$ bundle exec rake db:create

$ rails g migration create_suggestions
  --> invokes active record, creates the active record

inside the migration file (db/migrate)
  
  def change
    create_table :suggestions do |t|
      t.string :title, null: false
      t.text :box, null: false

      t.timestamps
    end
  end

$ be rake db:migrate
  check the schema.rb in the migrate file to check your progress
next create the model, then the controller

suggestions_controller.rb
  
  def hello
    render plain: 'hello'
  end

routes
  get '/hello', to 'suggetions#hello'
  (also, check out resources :suggestions, use this!) can specify with options too only [:values], or except to get rid of only a couple things

views/suggestions
  (dont render the view in your controller, just
    def hello
    end )
  then in hello.html.erb
    <h1> hello! </h1>

check with rails routes


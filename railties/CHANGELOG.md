## Rails 4.0.0 (unreleased) ##

*   Correctly handle SCRIPT_NAME when generating routes to engine in application
    that's mounted at a sub-uri. With this behavior, you *should not* use
    default_url_options[:script_name] to set proper application's mount point by
    yourself. *Piotr Sarnacki*

*   `config.threadsafe!` is deprecated in favor of `config.eager_load` which provides a more fine grained control on what is eager loaded *José Valim*

*   The migration generator will now produce AddXXXToYYY/RemoveXXXFromYYY migrations with references statements, for instance

        rails g migration AddReferencesToProducts user:references supplier:references{polymorphic}

    will generate the migration with:

        add_reference :products, :user, index: true
        add_reference :products, :supplier, polymorphic: true, index: true

    *Aleksey Magusev*

*   Allow scaffold/model/migration generators to accept a `polymorphic` modifier
    for `references`/`belongs_to`, for instance

        rails g model Product supplier:references{polymorphic}

    will generate the model with `belongs_to :supplier, polymorphic: true`
    association and appropriate migration.

    *Aleksey Magusev*

*   Set `config.active_record.migration_error` to `:page_load` for development *Richard Schneeman*

*   Add runner to Rails::Railtie as a hook called just after runner starts. *José Valim & kennyj*

*   Add `/rails/info/routes` path, displays same information as `rake routes` *Richard Schneeman & Andrew White*

*   Improved `rake routes` output for redirects *Łukasz Strzałkowski & Andrew White*

*   Load all environments available in `config.paths["config/environments"]`. *Piotr Sarnacki*

*   Add `config.queue_consumer` to allow the default consumer to be configurable. *Carlos Antonio da Silva*

*   Add Rails.queue as an interface with a default implementation that consumes jobs in a separate thread. *Yehuda Katz*

*   Remove Rack::SSL in favour of ActionDispatch::SSL. *Rafael Mendonça França*

*   Remove Active Resource from Rails framework. *Prem Sichangrist*

*   Allow to set class that will be used to run as a console, other than IRB, with `Rails.application.config.console=`. It's best to add it to `console` block. *Piotr Sarnacki*

    Example:

        # it can be added to config/application.rb
        console do
          # this block is called only when running console,
          # so we can safely require pry here
          require "pry"
          config.console = Pry
        end

*   Add convenience `hide!` method to Rails generators to hide current generator
    namespace from showing when running `rails generate`. *Carlos Antonio da Silva*

*   Scaffold now uses `content_tag_for` in index.html.erb *José Valim*

*   Rails::Plugin has gone. Instead of adding plugins to vendor/plugins use gems or bundler with path or git dependencies. *Santiago Pastorino*

*   Set config.action_mailer.async = true to turn on asynchronous
    message delivery *Brian Cardarella*

Please check [3-2-stable](https://github.com/rails/rails/blob/3-2-stable/railties/CHANGELOG.md) for previous changes.

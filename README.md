# TranslationEngine

```
gem 'translation-engine', git: 'https://github.com/blueberryapps/translation-engine.git'
```

## Configuration

Default configuration is that all part are turned off, so for enabling you need
to create file `config/initializers/translation_engine.rb` with this content:

```ruby
# config/initializers/translation_engine.rb

TranslationEngine.config do |config|
  # key for user
  config.api_key  = 'API_KEY'

  # url to Translation Server
  config.api_host = 'http://127.0.0.1:3000'

  # enable screenshot functionality
  config.use_screenshots  = true

  # enable to send translation after every request and receive translations
  # when something changed
  config.use_catcher      = true

  # If true TranslationEngine will throw exceptions on connection problems
  # If false TranslationEngine will just log exception to Rails.logger
  config.raise_exceptions = true
end
```

## Releases

```
# list all possible releases
I18n.backend.releases

# list all possible release which has same locale as I18n.locale
I18n.backend.current_locale_releases
```

## Screenshots Integration

### Javascript
Require javascript by inserting `app/assets/javascripts/application.js`
```
//= require translation_engine/screenshots
```
or in views `= javascript_include_tag 'translation_engine/screenshots'`
(this javascript is already precompiled, so you don't need to do anything else)

Ensure that you have jquery + coffeescript
(or similar gems which provides same function)

```ruby
gem 'coffee-rails'
gem 'jquery-rails'
```

### Stylesheets
Require stylesheets by inserting `app/assets/stylesheets/application.sass`:

```
@import translation_engine/screenshots`
```

or in views `= stylesheets_include_tag 'translation_engine/screenshots'`
(this stylesheet is already precompiled, so you don't need to do anything else)

### Start translations screenshoting
Create element with class `translation_engine_run`.
When you click on this element, Translation Engine will start screenshoting page
and then sends all images + highlights to server `/transaltion_engine` which
will be catched by `ScreenshotsMiddleware` and then send to TranslationServer.

or

Use callback `window.TranslationEngine.start()`

## Rake tasks

### `rake translation_engine:list:releases`

List all available releases from Translations Server


### `rake translation_engine:pull:master`

Download all master translations from Translations server and store them
into config/locales/z_translation_engine.yml

### `rake translation_engine:pull:release RELEASE=en_v001`

Download released translations from Translations server and store them
into config/locales/z_releases/(release_locale).yml,
will overwrite previous locale release, leaving allways only one release.

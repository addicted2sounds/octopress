---
layout: post
title: "Необходимые gems для rails"
date: 2015-04-25 08:49:47 +0300
comments: true
categories: ['Разработка', 'Ruby', 'Ruby on Rails']
---
Rails - замечательный фреймворк. С его использованием разработка становится легкой и приятной.

При разработке нового проекта постоянно приходится добавлять некоторые гемы. Ниже представлен обновляющийся список необходимых.
<!--more-->
###Haml
Вы еще не используете [HAML](http://haml.info/)? Для меня обычный Erb утрачен с его поялением. Попробуйте [tutorial](http://haml.info/tutorial.html) 

```
gem "haml-rails", "~> 0.9"

```
Для конвертации ваших erb в haml есть следущая команда:

```
rake haml:erb2haml
```

###Rspec
На Rails писать тесты [просто и приятно](http://rusrails.ru/a-guide-to-testing-rails-applications). С Rspec это делать еще легче. Если только знакомитесь с rspec, то обязательно прочитайте [это](http://betterspecs.org/ru/)

```
group :development, :test do
  gem 'rspec-rails'
end

```

С началом использования тестов, браузер при разработке используется все реже и реже. Для ин

```
rails generate rspec:install

```

###Factory Girl
Отличная замена стандартным фикстурам. Про "плюсы" использования написано уже предостаточно.

```
group :development, :test do
  gem 'factory_girl_rails'
end

```

[Официальный репозиторий](https://github.com/thoughtbot/factory_girl_rails). Для удобства можно добавить в `spec/rails_helper.rb`

```
config.include FactoryGirl::Syntax::Methods

```

###Faker
Можно и самому писать придуманные строчки и данные, но гораздо легче и приятней воспользоваться [Faker](https://github.com/stympy/faker)

```
group :development, :test do
  gem 'faker'
end

```

###Database cleaner
Не загрязнять нашу базу тестовыми данными поможет [Database Cleaner](https://github.com/DatabaseCleaner/database_cleaner). 

```
group :development, :test do
  gem 'database_cleaner'
end

```

Для подключения в проект редактируем `spec/spec_helper.rb`

```
RSpec.configure do |config|

  config.before(:suite) do
    DatabaseCleaner.strategy = :transaction
    DatabaseCleaner.clean_with(:truncation)
  end

  config.around(:each) do |example|
    DatabaseCleaner.cleaning do
      example.run
    end
  end

end
```

###Bootstrap
Для симпатичного внешнего вида лучшие косметологи мира рекомендуют [Bootstrap](http://getbootstrap.com/)

```
gem 'bootstrap-sass'

```

----
Поскольку эти гемы используются почти в каждом проекте, то при использовании rvm лучше установить их в глобальный gemset:

```
rvm @global do gem install rails haml-rails faker capistrano-rails factory_girl_rails database_cleaner

```

нужное - добавить, ненужное - убрать
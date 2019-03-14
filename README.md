# direct_message_smple

This app that is the direct message function for Rails.

## Building Step

```sh
% bundle init
% bundle install --path vendor/bundle --jobs=4
% bundle exec rails new . -B -T -C -d postgresql --skip-turbolinks
```

## Add Devise

`gem "devise"`

## Devise

```sh
% rails g devise:install
% rails g devise:controllers Users
% rails g devise user name:string
% rails g devise:views
```

## Migrate

```sh
% rails db:create
% rails db:migrate
```

## Models

```rb
rails g model room name:string
rails g model entry user:references room:references
rails g model message user:references room:references content:text
```

```rb
# app/model/user.rb
class User < ApplicationRecord
  # Include default devise modules. Others available are:
  # :confirmable, :lockable, :timeoutable, :trackable and :omniauthable
  devise :database_authenticatable, :registerable,
         :recoverable, :rememberable, :validatable
  has_many :messages, dependent: :destroy
  has_many :entries, dependent: :destroy
end
```

```rb
# app/model/entry.rb
class Entry < ApplicationRecord
  belongs_to :user
  belongs_to :room
end
```

```rb
# app/model/room.rb
class Room < ApplicationRecord
  has_many :messages, dependent: :destroy
  has_many :entries, dependent: :destroy
end
```

```rb
class Message < ApplicationRecord
  belongs_to :user
  belongs_to :room
end
```

## Controllers

```sh
% rails g controller users index show
% rails g controller rooms
% rails g controller messages
```


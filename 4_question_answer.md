# This is an explanation of how to use "singular" and "plural" properly in Rails.

## Question
> For example, "blogs" is specified for parameters when creating a controller, and "blog" is specified for parameters when creating a model. It seems that various variables are automatically created based on that, so I think it makes sense to use "blogs" and "blog" properly, but it is still confusing because there is no description anywhere.   
Even if I try "rake routes", there are "blog" "new_blog" "blogs" and "confirm_blogs" in Prefix. I don't understand why this is happening at all.  

## Answer 

Rails is built on conventions, and when those conventions are broken, so is your application. The logic behind rail naming conventions is simple

### Rails Generators

```
rails g model User name
```
Model names are singular : models represent a single instance.

```
rails g controller Games name
```
Controller names are either singular or plural : Using “rails g resource” names the controllers plural, which makes sense because I think about them controlling many routes.

```
rails g resource player name
```
Resource names are singular : They create a lot of mvc framework, the name you pass will become the model name, and let rails pluralize the rest.

```
rails g migration create_players name:string
```
Migrations are plural : technically this is just a name for a migration file, but when rails builds them for itself, it is plural. This file will build a table, and table names are plural.

### Routes

```
Rails.application.routes.draw do
resources :users
resources :games
resources :players
End
```
Resource routing is plural : both the word resources is plural, as you are mapping many routes at once, and the variable name is plural.


```
get '/players', to: 'players#index', as: 'players'
get '/players/new', to: 'players#new', as: 'new_player'
get '/players/:id', to: 'players#show', as: 'player'
post '/players', to: 'players#create'
get '/players/:id/edit', to: 'players#edit', as: 'edit_player'
patch '/players/:id', to: 'players#update'
delete  '/players/:id' to: 'players#destroy'
```
### Strong Params
```
def user_params
params.require(:user).permit(:name)
End
```
Params required key is singular : the key refers to a singular post/patch/put request for an instance. I suppose there is a time where this could be plural, but I cannot find any yet, and ruby on rails documentation only shows it being singular.

### Views


View directories are plural : there are many views.

View files however are singular : they render a single view. 
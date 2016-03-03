# ROR_session_app_1

Description: This APP is a small sample, where a User can blog

## Make a CRUD operations of USER

**Run the Command**
```sh
$ rails generate scaffold user name age:integer email
```

## Make a CRUD operations of ARTICLE

**Run the command**

```sh
$ rails generate scaffold article title content:text user:references
```


## Lets make the root of site to user list and inherit the article route in user route

**Change in config/routes.rb**. 

Un-comment line no. 8 and change it to:
```sh
  # resources :articles
  resources :users, shallow: true do
    resources :articles
  end
```

Change the routes in line 2,3 to 
```sh
 root 'users#index'
```


## Run Migrations to make tables in Db

```sh
 $ rake db:migrate
```

## Make a join between User and Article in models

**Add the below line to file "app/models/user.rb" before end

```sh
 	has_many :articles
```

## Lets make a graphical design of the database

```sh
 	$ bundle exec erd
 	$ sudo apt-get install graphviz
 	$ rake diagram:all
```

**Note:** Check the file "erd.pdf" and folder "doc"

## Lets start our Rails server

```sh
 	$ rails server
```


## Add the below line to file "app/views/users/show.html.erb" after line no. 17
**ERROR**
```sh
 	</br>
	</br>
	</br>
	<%= link_to @user.name + ' articles', user_articles_path(@user) %>
	</br>
	</br>
	</br>
```

## Change the line in file "app/views/articles/index.html.erb" at line no. 31 to 
**ERROR**
```sh
 <%= link_to 'New Article', new_user_article_path %>
```


## Change the code in function "NEW" in file "app/controllers/articles" to 
**ERROR**
```sh
  @user = User.find(params[:user_id])
  @article = @user.articles.new
```


## Change the line in file "app/views/articles/_form.html.erb" at line 1 to 
**ERROR**
```sh
  <%= form_for([@user, @article]) do |f| %>
```


## Change the line in file "app/views/articles/_form.html.erb" at line 22 to 
**Functionality:** User ID is visible, lets hide it
```sh
  <div class="field" style="display:none">
```


## Change the line in file "app/views/articles/new.html.erb" at line 5 to 
**ERROR**
```sh
  <%= link_to 'Back', user_articles_path %>
```

## Change the process of saving article with user. Add and modify code in file "app/controllers/
articles" at line 28 to
**ERROR**

```sh
  @user = User.find(params[:user_id])
  @article = @user.articles.new(article_params)
```

## Change the line in file "app/views/articles/show.html.erb" at line 19 and in file 
**ERROR**
"app/views/articles/edit.html.erb" at line 6 to 
```sh
  <%= link_to 'Back', user_articles_path(user_id: @article.user.id) %>
```


## Add line in file "app/views/articles/index.html.erb" at line 32
**Functionality:** Link in Article List which redirects to User List
```sh
  <%= link_to "All Users",  users_path %>
```

## Now Time to move our build on production
```sh
  $ bundle install --without production
  $ git add .
  $ git commit -a -m "Update Gemfile.lock for Heroku"
  $ heroku create
  $ git push heroku master
  $ heroku run rake db:migrate
  $ heroku apps:rename paxcel-session-app
```



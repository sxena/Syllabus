# React-Rails

Up until this point, we've been using create-react-app to build our applications, and we've been using a separate Rails applications to explore Rails and APIs.  Have you wondered if Rails, as full featured as it is, could be the platform for the API and the React app together?  If so, it was a good question to ask, and as you may have guessed, Rails can also serve right from normal old erb pages.  Not only can it do so, but the solution is very elegant, and using Rails in this way allows us as developers to build larger and more interesting applications in an organized way.

Let's explore how Rails and React are integrated by constructing the simplest possible Rails app, and the simplest possible React component and getting them to work together.

## React-Rails Docs
Please have a read of the [docs for the react-rails project](https://github.com/reactjs/react-rails) first to see what we're going to do, and all of the advanced features of the gem.

## Devise docs
The Devise documentation is also great. Devise is so flexible and ubiquitous, that this page probably deserves a spot in your bookmarks.  [Devise](https://github.com/plataformatec/devise)

## About authentication
1. [Authentication vs. Authorization](./02-authorization-and-authentication/01-authentication-vs-authorization.md)
2. [How Authentication Works](./02-authorization-and-authentication/02-authentication.md)

## Guides

1. [Stand Alone Devise App](./02-authorization-and-authentication/03_devise.md)
2. [React and Rails Together](./01-react-in-rails/02_Hello_World.md)
2. [Single Page React App in Rails](./01-react-in-rails/03_single_page_app.md)
3. [Putting it all together](./03_devise_and_react_together.md)





### A Word about Devise
If you are changing the columns on your User model that is using Devise, and you want to add those params to the user registration form, you need to let Devise know about the new parameters.  Devise doesn't normally expose its controller methods to us to update the strong params like we would another controller, so we need to handle it a bit differently.  To do this for the example above of adding first_name and last_name, we update the ApplicationController like so:

```ruby
class ApplicationController < ActionController::Base
  before_action :configure_permitted_parameters, if: :devise_controller?

  protected

  def configure_permitted_parameters
    devise_parameter_sanitizer.permit(:sign_up, keys: [:first_name, :last_name])
  end
end
```

You can [read more about Devise and strong params here](https://github.com/plataformatec/devise#strong-parameters).

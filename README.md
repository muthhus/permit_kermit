PermitKermit
=============

Simple plugin for role-based permissions

## Usage

Include module to your base controller (e.g. AdminController)

```ruby
include PermitKermit
```

Optionally define route where user should be redirected in case of no permissions:

```ruby
self.permission_denied_route = :admin
```
when permission_denied_route is not defined `root_url` will be used.

Use as before_filters in controller:

```ruby
permit :admin, :moderator, :expect => :destroy
permit :admin, :only => :destroy
```

or in views:

```erb
<nav>
<%= link_to t('.nav.reviews') users_path %>
<% permit :admin do %>
  <%= link_to t('.nav.users') users_path %>
<% end %>
</nav>
```

### Important note!
**PermitKermit** expects controller to have `current_user` variable which responds to `role_names` returing array with symbolized or stringified role names, e.g:

```ruby
  def role_names
    @role_names ||= self.roles.map(&:name)
  end
```
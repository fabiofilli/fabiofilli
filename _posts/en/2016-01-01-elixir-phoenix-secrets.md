---
layout: post
title:  "Elixir Phoenix - Secrets"
date:   2015-05-15
author: Fabio Filli
lang: en
---
Sometimes it’s important to have secrets! Let’s say you’re working on an open source Elixir Phoenix application with git as version control system, you don’t want to share your sensitive configuration details (such as passwords or API Keys). And now?

Easy, you can set environment variables or you create a file that works like `config/prod.secret.exs`.

Create a new file in config, name it `config.secret.exs` and put all configurations in your new created file `config/config.secret.exs`, which will apply to all environments.

`config/config.secret.exs`

```elixir
	use Mix.Config

	config :your_app_name,
	    some_key: "543218765164d64fa654654"
	    some_other_key: "another_long_secret_string"
```

Import `config/secret.exs` into your regular `config/config.exs` file.

`config/config.exs`

```elixir
	# Import environment specific config. This must remain at the bottom
	# of this file so it overrides the configuration defined above.
	import_config "#{Mix.env}.exs"
	import_config "config/secret.exs"
```

Don’t forget to hide the new `config/config.secret.exs` file! Add it in your `.gitignore` file.

`.gitignore`

```elixir
	# The config/prod.secret.exs file by default contains sensitive
	# data and you should not commit it into version control.
	#
	# Alternatively, you may comment the line below and commit the
	# secrets file as long as you replace its contents by environment
	# variables.
	/config/prod.secret.exs
	/config/config.secret.exs
```

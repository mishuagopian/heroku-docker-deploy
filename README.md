# Heroku Docker Deploy - GitHub Action

Build, Push and Release a Docker container to Heroku 🚀.

**Important:**
Forked from [gonuit/heroku-docker-deploy](https://github.com/gonuit/heroku-docker-deploy), the fork add the possibility to omit the release phase. This will allow users to release the generated image when desired.
  
## Getting started

### Your GitHub action workflow file might look like this:
```yml
# Your workflow name.
name: Deploy to heroku.

# Run workflow on every push to master branch.
on:
  push:
    branches: [master]

# Your workflows jobs.
jobs:
  build:
    runs-on: ubuntu-latest
    steps:
      # Check-out your repository.
      - name: Checkout
        uses: actions/checkout@v2


### ⬇ IMPORTANT PART ⬇ ###

      - name: Build, Push and Release a Docker container to Heroku. # Your custom step name
        uses: gonuit/heroku-docker-deploy@v1.3.3 # GitHub action name (leave it as it is).
        with:
          # Below you must provide variables for your Heroku app.

          # The email address associated with your Heroku account.
          # If you don't want to use repository secrets (which is recommended) you can do:
          # email: my.email@example.com
          email: ${{ secrets.HEROKU_EMAIL }}
          
          # Heroku API key associated with provided user's email.
          # Api Key is available under your Heroku account settings.
          heroku_api_key: ${{ secrets.HEROKU_API_KEY }}
          
          # Name of the heroku application to which the build is to be sent.
          heroku_app_name: ${{ secrets.HEROKU_APP_NAME }}

          # (Optional: true | false, default: false)
          # Determine if Heroku release phase should be skiped
          heroku_skip_release: false

          # (Optional, default: "./")
          # Dockerfile directory.
          # For example, if you have a Dockerfile in the root of your project, leave it as follows:
          dockerfile_directory: ./

          # (Optional, default: "Dockerfile")
          # Dockerfile name.
          dockerfile_name: Dockerfile

          # (Optional, default: "")
          # Additional options of docker build command.
          docker_options: "--no-cache"

          # (Optional, default: "web")
          # Select the process type for which you want the docker container to be uploaded.
          # By default, this argument is set to "web".
          # For more information look at https://devcenter.heroku.com/articles/process-model
          process_type: web
          
   
          
### ⬆ IMPORTANT PART ⬆ ###
```

## Logs
### All build logs will be grouped:
![An example of logs groups.](readme/groups.png)
### And available to you.
![Logs example.](readme/logs.png)

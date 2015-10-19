### Get Started - FishFish Shell

    # Only configure this first line. Must start with upper case letter.
    set BOOTSKETCH_NAME YourNewProjectName

    # The rest should be safe to copy & paste...
    set BOOTSKETCH_NAME_UPPER (echo $BOOTSKETCH_NAME | tr "[:lower:]" "[:upper:]")

    # Clone RailsBootsketch
    git clone git@github.com:emcmanus/RailsBootsketch.git $BOOTSKETCH_NAME
    cd $BOOTSKETCH_NAME
    git remote rm origin

    # Update project name
    sed -i '' "s/RailsBootsketch/$BOOTSKETCH_NAME/g" **.rb **.yml **.html.erb
    sed -i '' "s/RAILSBOOTSKETCH/$BOOTSKETCH_NAME_UPPER/g" **.rb **.yml
    git commit -am "Update project name."

    # Rails/DB setup
    bundle install
    rake db:setup
    rails generate simple_form:install --bootstrap

    # Create unique, local secret
    echo "SECRET_KEY_BASE="(rake secret) > .env

    echo "" > README.markdown
    git commit -am "Remove README"

    # Done!
    foreman start

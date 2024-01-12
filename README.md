### Scripts and guide on how to deploy Klaxon on your own server

[Klaxon](https://github.com/themarshallproject/klaxon) enables reporters and editors to monitor scores of sites on the web for newsworthy changes.

To deploy klaxon using this repo you'll need `docker` and `docker-compose`.
This method uses Gmail as email notification server, so you'll also need a gmail account.

#### Steps:
1. create an application password for the gmail account that will act as notifier
    - go to https://myaccount.google.com/apppasswords
    - add a new application and save the generated password (16 characters)

2. edit `.env` and provide values for the following vars
    - `SECRET_KEY_BASE` - add a randomly generated password
    - `POSTGRES_PASS` - add a randomly generated password
    - `GMAIL_USERNAME` - the email address which acts as sender/notifier (see step 1.)
    - `GMAIL_PASSWORD` - the password generated at step 1. (but dont forget to delete any white spaces)

3. create the folder for database persistence with `mkdir pgdata` and fetch the klaxon source code with `git submodule update --recursive`

4. start the stack using `docker-compose up` in a separate terminal
    - the klaxon container will be built on the first run
    - when it's done, you should be able to access its web interface at http://localhost:3000

5. find out the klaxon's container name useing `docker ps`; should be something like `klaxon-deploy_klaxon_1`

6. in a new terminal access the klaxon container using `docker exec -it <container-name> bash`

7. add an admin user using the command `bundle exec rake users:create_admin RAILS_ENV=production ADMIN_EMAILS=<your_admin_email>`

8. enter the admin email in the web interface and check your email for a login link; you should now have access to the administration dashboard

## <center>👾</center>
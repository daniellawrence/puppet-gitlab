This file is a work in progress

#Common Errors
================

##Error 500 
http://f.cl.ly/items/0g253M0q3W290G1T0s2y/Image%202013.10.03%208%3A35%3A15%20PM.png    
Look at /home/git/gitlab/log/production.log  


If you see the following error, then the project is public, but the user is not part of the group  

    NoMethodError (undefined method `id' for nil:NilClass):  
      app/controllers/public/projects_controller.rb:22:in `show'  

*Solution: Add user to group (with atleast reporter permission), or make project private  
*Solution2: Access the project from the dashboard  
*Solution3: Wait for gitlab 6.2 to resolve this bug

http://gitlab.somedomain/admin/groups/company

##Push prompts for git@foo password
Check the following:  
1. Is the hostname and shortname configured correctly (gitlab.yml, /etc/hosts, ect..)  
2. Is the git config --global configured  
3. Does the .ssh folder have the correct permissions  
4. Does the user have their ssh keys saved into gitlab?   
5. Does the repo actually have a file to push? 

You will most likely need to reinstall gitlab and make sure the hostname is correct
http://stackoverflow.com/questions/18501874/gitlab-prompts-for-password-while-push-for-git-user

##Thumbnail icon won't change  
- Clear the cash in your browser  
- Run `service gitlab reload` or `service gitlab restart`  
- Restart the server  
- Verify the icons in /home/git/ exist
  
  
# Installation locations

Git lab is installed to /home/git/gitlab
Git lab shell is installed to /home/git/gitlab-shell




# Logging


ngninx logs are located in the following directories: 

/var/log/nginx/access.log
/var/log/nginx/error.log
/var/log/nginx/gitlab_access.log
/var/log/nginx/gitlab_error.log

gitlab logs are located in the following locations

/home/git/gitlab/log/application.log  
/home/git/gitlab/log/production.log  
/home/git/gitlab/log/sidekiq.log  
/home/git/gitlab/log/unicorn.stderr.log  
/home/git/gitlab/log/unicorn.stdout.log


# Pitfalls

Verify that /etc/nginx/sites-available/gitlab has a wildcard infromt of the server

bad
listen 80;

good
listen *:80 default_server;



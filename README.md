# Problem to solve
Some students have set up the homework to have the ubuntu shell with the Vagrant VM goodness as the root folder, with the assignment inside the `code` folder.  This works great locally, but deploying to Heroku breaks.  Heroku wants some files in the root folder so their buildpacks work.

# Solution
In short, I followed the instructions here.  This got me 90% there:
https://lostechies.com/derickbailey/2013/09/17/making-heroku-run-a-nodejs-app-from-a-sub-folder/

A little bit of debugging off of some surprisingly helpful Heroku troubleshooting docs finished the job.

Specific steps:
- moved the `package.json` to the root folder
- updated the `package.json` file to have a "node" engine that matches the version on my machine.
- added `"start": "node code/server.js"` to the "scripts" section in the `package.json` per the advice of the lostechies.com website.  It's not necessary, but it's pretty nifty.
- added a `Procfile` that points Heroku to to the server file inside the `code` folder.
- added a `.gitignore` file that removes the `node_modules` from the repo.  Heroku will complain and break if the repo contains `node_modules`, since the build process 

Disclaimer: I deployed using the GUI on heroku.com, rather than the CLI.  The CLI shouldn't cause any additional issues, but it might.
# NPM Project As A Service
(No root required) Adds npm project to start on system boot (with/without forever) or on scheduled (such as npm/git updates daily). 

# Installation

There are 3 ways to use npm-as-service

Install globally: (for user level versions of npm such as nvm)
````
npm install npm-as-service -g
````

Install globally as root: (for system level versions of npm such as n and npm from system repos)
````
sudo npm install npm-as-service -g
````

Use in your project only:
````
npm install npm-as-service --save
PATH=$PATH:node_modules/npm-as-service/bin
````
# Usage

## Start your project on boot

In your project root where package.json is located:
````
npm-service install
````

You must then edit your package.json to specify your start command

package.json:
```
{
  ...
  "main": "index.js",
  ....
  "scripts": {
    "start": "node ${npm_package_main}",
   }
   ...
```

You can also use forever

package.json:
```
{
  ...
  "main": "index.js",
  ....
  "scripts": {
    "start": "forever start ${PWD}/${npm_package_main}",
   }
   ...
```
## Automaticly (daily) update your project including security issues with dependencies
```
npm-service install --cmd npm update --crontab_time @daily
npm-service install --cmd npm audit fix --crontab_time @daily
```

# todo
- Unit testing
- Test other platforms
- Other service starting methods
- Detect help install crontab
- 'npm-service init' to edit pacakge.json (detect forever, postinstall, remove, rootless)
- 'npm-service init-insecure' to edit pacakge.json (disable updates)
- Example project

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
PATH=$PATH:node_modules/.bin
````
# Usage

## Start your project on boot

In your project root where package.json is located run:
````
npm-service install
````

If you don't have a package.json in your project root you can run:
````
npm init
````

You must then edit your package.json to specify your start command

package.json: (minimal)
```
{
  ...
  "main": "index.js",
  ....
  "scripts": {
    "start": "node ${npm_package_main}",
   }
   ...
}
```

package.json:  (using forever)
```
{
  ...
  "main": "index.js",
  ....
  "scripts": {
    "start": "forever start ${PWD}/${npm_package_main}",
   }
   ...
}
```
## Automaticly (daily) update your project including security issues with dependencies
```
npm-service install --cmd npm update --crontab_time @daily
npm-service install --cmd npm audit fix --crontab_time @daily
```

## How to remove services
```
npm-service remove
npm-service remove --cmd npm update --crontab_time @daily
npm-service remove --cmd npm audit fix --crontab_time @daily
```

## More help:
```
$ npm-service --help
Usage: npm-as-service [options] [command]

Options:
  -V, --version      output the version number
  -h, --help         display help for command

Commands:
  install [options]  install npm package as a service
  remove [options]   remove npm package as a service
  help [command]     display help for command
```

## Install help:
```
$ npm-service install --help
Usage: npm-as-service install [options]

install npm package as a service

Options:
  -c, --cmd <command...>            The command to use for cron (default: ["npm","start"])
  --prefix <path>                   npm --prefix (default: "/home/owner/Documents/repos/npm-as-service")
  -t, --crontab_time <time>         Comma separated time specification list or nickname {m h dom mon 
                                        dow,@reboot,@yearly,@annually,@monthly,@weekly,@daily,@hourly}. see "man crontab(5)" 
                                        (default: "@reboot")
  -p, --cron_paths <PATH:PATH:...>  Extra environment paths for cron. For example where npm is located. 
                                        (default: "/usr/local/sbin:/usr/local/bin:/sbin:/bin:/usr/sbin:/usr/bin")
  -l, --cron_log <PATH>             Path to cron log
  -v, --verbose                     Verbose debug output
  -h, --help                        Display help for command
```


# todo
- Unit testing
- Test other platforms
- Other service starting methods
- Detect help install crontab
- 'npm-service init' to edit pacakge.json (detect forever, postinstall, remove, rootless)
- 'npm-service init-insecure' to edit pacakge.json (disable updates)
- Example project

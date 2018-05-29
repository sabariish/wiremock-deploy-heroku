# wiremock-deploy-heroku
Deploy the wiremock jar to heroku.

Assumes you already have a heroku account, already have the heroku cli installed, and are logged into the heroku cli.

## Instructions

- Create a heroku application
```
heroku create <name>
```

- Add the [Energized Work](http://www.energizedwork.com) downloadable jar buildpack
```
heroku config:set 'NO_PRE_DEPLOY=true'
heroku buildpacks:set https://github.com/energizedwork/heroku-buildpack-runnable-jar
```

- Start the application
```
git push heroku master
```

- Check it
```
curl -X POST http://<name>.herokuapp.com/__admin/mappings -d '{ "request": { "method": "GET", "url": "/" }, "response": { "body": "Hello world!" }}'
curl http://<name>.herokuapp.com/
```

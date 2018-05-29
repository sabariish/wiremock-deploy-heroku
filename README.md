# wiremock-deploy-heroku
Deploy wiremock to heroku.

Assumes you already have a heroku account, already have the heroku cli installed, and are logged into the heroku cli.

## Instructions

- Create a heroku application
```
heroku create <name>
```

- Add the [Energized Work](http://www.energizedwork.com) downloadable jar buildpack. This will pull the wiremock jar defined as the ARTIFACT_URL property in the manifest.sh
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

With a json body returned
```
curl -X POST http://<name>.herokuapp.com/__admin/mappings -d '{ "request": { "method": "GET", "url": "/" }, "response": { "jsonBody": {"Hello": "world!" }}}'

curl http://<name>.herokuapp.com/
```

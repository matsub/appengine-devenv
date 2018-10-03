# appengine-devenv
Bunch of Dockerfiles to test App Engine Standard Environment with google-cloud-sdk

# For what?
These docker environments are used for testing App Engine's environment.

e.g. with wercker

```
test:
  box: matsub/appengine-python3
  steps:
    - script:
      name: install nose
      code: apk add --update py-pip && pip install nose

    - script:
      name: run app server in background
      code: dev_appserver.py --application=project_id app.yaml &

    - script:
      name: execute nosetests
      code: nosetests
```

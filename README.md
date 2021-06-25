# Wagtail Base

`Starting from scratch.` 

You need to create the poetry stuff first becuse poetry is run inside the containers later on and saves running it locally. But local install helps with vscode intellisense etc.

`.gitignore` should be swapped out for the .gitignore-project in your project.

## Start a temporary docker container:

    docker run --rm -it --workdir /code --volume "$(pwd):/code" python:3.8.5-slim bash

and run

    pip install poetry

    poetry init

Answer the questions and add the packages you need. You can always run this later in the main docker container but for now we need a `pyproject.toml` and `poetry.lock` file before running the main docker container.

If you don't add any packages run

    poetry lock

to create the `poetry.lock` file

-- Note: the .python-version should match the python version used in the docker file if possible, it means your local virtual env if you create one will be on the same verion.

---

### Optional and depends on what python packages you are using, I'm using Wagtail CMS with codyhouse frontend

With Wagtail installed via poetry and the docker container still running, run 

    poetry shell

    wagtail start wagtailcms .

You can stop the temporary container now.

    exit

Entirely optional but I move these folders and files around

    /wagtailcms/wagtailcms/** up one level and remove left over folder
    /wagtailcms/Dockerfile remove
    /wagtailcms/.dockerignore up one level
    /wagtailcms/manage.py up one level
    /wagtailcms/requirements.txt remove

and swap out the .gitignore file for .gitignore-project file

# Frontend (Codyframe)

Run

    ./get_frontend.sh

to setup the `frontend` folder and `package.json` at the site root

In the gulp file update the css and js paths to suit wagtailcms

    nvm use && npm install

Run

    npm run gulp watch

to start compiling the frontend into wagtailcms/static
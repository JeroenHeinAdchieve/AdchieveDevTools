# Support for Extra Services

Symfony Docker is extensible. When you install a compatible Composer package using Symfony Flex,
the recipe will automatically modify the `Dockerfile` and `compose.yaml` to fulfill the requirements of this package.

The currently supported packages are:

* `symfony/orm-pack`: install a PostgreSQL service
* `symfony/mercure-bundle`: use the Mercure.rocks module shipped with Caddy
* `symfony/panther`: install chromium and these drivers
* `symfony/mailer`: install a Mailpit service
* `blackfireio/blackfire-symfony-meta`: install a Blackfire service

> [!NOTE]
> If a recipe modifies the Dockerfile, the container needs to be rebuilt.

> [!WARNING]
> We recommend that you use the `composer require` command inside the container in development mode so that recipes can be applied correctly

## What is Symfony flex?

Symfony Flex is a Composer plugin used in Symfony applications to manage dependencies and configurations, including
so-called Flex recipes. These recipes automate the installation and configuration of Symfony bundles and related
components. When you add a package using composer require, Symfony Flex checks if there's a recipe associated with that
package and applies any necessary modifications to your Symfony project. This is why it is recommended to run `composer
require` inside the container so that Symfony flex can modify the composer.json, Dockerfile and other configuration
files correctly within the Dockerized environment.

## How could you do this?

Let's say you want to add the `symfony/orm-pack` to your Symfony project, this is how you could do it.

1. Access your Docker container where your Symfony application is running: `docker exec -it my-symfony-app-container bash`
2. Run composer require `composer require symfony/orm-pack`
3. If Flex modifies the Docker configuration (Dockerfile, docker-compose.yaml), rebuild the Docker containers to apply these changes: `docker-compose up --build`


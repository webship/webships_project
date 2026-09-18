# Webships Project

A ready-to-use Drupal API project.

The site serves a JSON:API from `/api`, with authentication, authorization and
OpenAPI documentation rendered by Swagger UI at `/api-docs`. Everything comes
from drupal.org.

The project requires only the [Webships](https://www.drupal.org/project/webships)
installer and two site templates. The installer lists them:

- [Webships Starter](https://www.drupal.org/project/webships_starter): the
  default site template for Webships, with the apps and organizations content
  model and its API resources.
- [WebAPI Starter](https://www.drupal.org/project/webapi_starter): the basic
  default Drupal API site template, with the standard content model.

Both use the Drupal core administration theme, for the back end and the front
end.

## Create a project

Composer runs inside DDEV, so nothing is needed on your machine but DDEV itself.

```shell
mkdir -p ~/workspace/projects/my-api
cd ~/workspace/projects/my-api
ddev config --project-type=drupal11 --docroot=web --php-version=8.4
ddev start
ddev composer create-project drupal/webships_project:^1.0
```

## Install the site

Open the site and follow the installer, where you pick the site template:

```shell
ddev launch
```

Or install from the command line, with the Webships Starter site template:

```shell
ddev drush si -y webships --account-name=webmaster --site-name="My API" installer_site_template_form.add_ons=webships_starter
```

Use `webships_starter` or `webapi_starter` as the site template.

## Project layout

| Path | Content |
|---|---|
| `web/` | Drupal root (core, contrib modules and themes) |
| `web/profiles/contrib/webships` | The Webships installer |
| `web/libraries/swagger-ui/dist` | Swagger UI, for the API documentation |
| `recipes/webships_starter` | The Webships Starter site template |
| `recipes/webapi_starter` | The WebAPI Starter site template |
| `vendor/` | Composer dependencies, Drush |

## What is inside

- Drupal core 11.4.
- [Web API](https://www.drupal.org/project/webapi): JSON:API from `/api`,
  read-only, with OAuth 2.0 and consumers.
- OpenAPI documents for JSON:API and REST, rendered with Swagger UI.

## Write operations

JSON:API is read-only. Turn write operations on at
`/admin/config/services/jsonapi` only when the site needs them, and rebuild the
cache afterwards.

## Cross-origin requests

CORS lives in `sites/default/services.yml` under `cors.config`. No module can
ship it, so set it per site.

## Maintainers

- Rajab Natshah: [RajabNatshah](https://www.drupal.org/u/rajabnatshah)

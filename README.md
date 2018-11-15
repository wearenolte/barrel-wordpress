# Nolte WordPress Upstream

This is a WordPress repository configured to run on the [Pantheon platform](https://pantheon.io).

Pantheon is website platform optimized and configured to run high performance sites with an amazing developer workflow. There is built-in support for features such as Varnish, Redis, Apache Solr, New Relic, Nginx, PHP-FPM, MySQL, PhantomJS and more. 

This image will also work on any other platform provided a `wp-config-local.php` file is included rather than by modifying `wp-config.php`. Certain mu-plugins for Pantheon should be replaced with platform-specific ones.

## Getting Started with Pantheon 

The below pertains mostly to setting up a brand new site. For most developers, these steps will be completed. 

### 1. Spin-up a site

If you do not yet have a Pantheon account, you can create one for free. Once you've verified your email address, you will be able to add sites from your dashboard. 

- Go to Organizations > Nolte > Upstreams
- Click the "create site from upstream" button next to Nolte's WordPress Upstream. The name is important. The name of the site will be handleized (converted to lower case with non-alphanumerics replaced with hyphens), which will then be used for the Pantheon environment urls as well as the bitbucket repo, which must be created next. Use site's domain name (without the suffix) if known.

### 2. Load up the site

When the spin-up process is complete, you will be redirected to the site's dashboard. Click on the "Install WordPress" button to continue.

### 3. Run the WordPress installer 

Follow steps to setup the new WordPress site by visiting the admin for the first time.

- Populate the Site Title using the product name.
- The initial user should be `nolte`.
- The initial user’s email should be `developer@wearenolte.com`.
- The password should be random-generated using the LastPass generator set to 16 character lenght or more.
- Immediately save these credentials to the shared LastPass folder for this product.
- Protect multidev, dev, test, and live (if pre-launch) environments with basic authentication to prevent bots and crawlers from indexing the site using the following credentials: username ("nolte") and password ("nolte101")

If you would like to keep a separate set of configuration for local development, you can use a file called `wp-config-local.php`, which is already in our `.gitignore` file.

### 4. Developer: Repository Setup & Synchronization

Pantheon's initial codebase needs to be synchronized with Bitbucket, which is used as the truth respository. Follow these steps:

- Create a new private bitbucket repo in the client's project (create a new project if this is the first repo for this client) in the WeAreNolte team. Use the same name as handleized by Pantheon. For instance, “new-site” will be both the bitbucket repo name and the Pantheon project name, which would come in the form of `dev-new-site.pantheonsite.io`.
- Go to the Pantheon dashboard (dev environment), click the "clone with git" button and copy the clone command.
- Clone the Pantheon repo onto your local machine using `-o pantheon` parameter, eg `git clone ssh://codeserver.dev.b540751e-85f4-4061-870e-db63ed4e6d6a@codeserver.dev.b540751d-84f4-4072-871e-db63ec4d6d6a.drush.in:2222/~/repository.git testing-barrel -o pantheon`.
- Update the `name` and `config.site` parameters in the `.lando.yml` file to match the handleized name from Pantheon, then commit the changes.
- Add the Bitbucket remote as "origin", eg `git remote add origin git@bitbucket.org:WeAreNolte/testing-barrel.git`.
- Push to Bitbucket, eg `git push -u origin master`.
- Run `lando start` to spin up your local develoment environment.

You should use [Lando](https://docs.devwithlando.io/installation/installing.html) for local development, click the link for installation instructions if you don't have it already.

#### Continuous Integration

... Coming soon!

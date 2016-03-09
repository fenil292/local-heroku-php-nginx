## local-heroku-php-nginx

Example Vagrantfile and application showing local execution of [`heroku-buildpack-php`](https://github.com/heroku/heroku-buildpack-php) using `heroku-php-nginx` on Ubuntu 14.04. LTS.

```sh
git clone git@github.com:jonahgeorge/local-heroku-php-nginx
cd local-heroku-php-nginx

vagrant up # Time for ☕️

vagrant ssh
cd /vagrant

composer install

foreman start
```

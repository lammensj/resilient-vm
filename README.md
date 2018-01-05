<p align="center"><img width=50% src="https://raw.githubusercontent.com/lammensj/resilient-vm/master/assets/images/logo.jpg"></p>

# [Project name]

[Project description]]

## Getting Started

These instructions will get you a Drupal 8 project up and running on your local machine for development and testing purposes.

### Prerequisites

All you need is [Composer](https://getcomposer.org/) and [Vagrant](https://www.vagrantup.com/) installed on your laptop or pc. Every other service will be downloaded inside the virtual machine.

```
$ composer install
```

### Installing

Default settings regarding the VM can be found in `./config`. The following files are present:
 - `config.yml`: configuration independent of the project (eg. synced folders, ports, composer etc.)
 - `default.local.config.yml`: configuration about the project (eg. name, credentials etc.)

```
$ cp ./config/default.local.config.yml ./config/local.config.yml
```

Adjust the lines in `./config/local.config.yml` which are not commented to match your project.

#### A. Starting fresh

Uncomment the lines below `# Installing from scratch` in `./config/local.config.yml`.

#### B. Starting from existing configuration

Uncomment the lines below `# Installing from existing configuration` in `./config/local.config.yml`.

#### Run Vagrant

All there is left to do, is start Vagrant and let it do its thing.
```
$ DRUPALVM_ANSIBLE_ARGS='--extra-vars "drupal_install_site=true"' vagrant up
```

This will download a [Vagrant](https://www.vagrantup.com/) machine (Debian9) and provision it using [Ansible](https://www.ansible.com/). Inside, a [Resilient](https://github.com/lammensj/resilient-project)-distribution will be installed. If everything is finished, go to the url you set up in `./config/local.config.yml` under `vagrant_hostname`.

## Credentials

### Connecting to MySQL
- MySQL Host: `127.0.0.1`
- Username: `drupal` (unless overridden by `drupal_db_user`)
- Password: `drupal` (unless overridden by `drupal_db_password`)
- SSH Host: `192.168.88.88` (unless overridden by `vagrant_ip`)
- SSH User: `vagrant` (unless overridden by `vagrant_user`)
- SSH Key: (browse to your `~/.vagrant.d/` folder and choose `insecure_private_key`)

### Drupal
- Username: `admin` (unless overridden by `drupal_account_name`)
- Password: the default is `admin` but please change this when going to production (unless overridden by `drupal_account_pass`)

## Built With

* [Drupal 8](https://www.drupal.org/) - Drupal 8
* [Resilient](https://github.com/lammensj/resilient-project) - Resilient distribution
* [Gulp](https://gulpjs.com/) - Automated frontend workflow

## Workflow

### Config management

Hence the fact that we're using [Config Split](https://www.drupal.org/project/config_split) to break apart certain config (eg. only enable Devel in development) we must use the drush commands provided by that module. Use `$ drush csex -y` to export and `$ drush csim -y` to import configuration files.
You can enable development config by adding `$config['config_split.config_split.dev']['status'] = TRUE;` in `./htdocs/web/sites/default/settings.local.php`.

### Versioning

We use [Gitflow](http://nvie.com/posts/a-successful-git-branching-model/) for versioning.

## Authors

* **Jasper Lammens** - *Initial work* - [lammensj](https://github.com/lammensj)

## License

This project is licensed under the MIT License - see the [LICENSE](LICENSE) file for details.


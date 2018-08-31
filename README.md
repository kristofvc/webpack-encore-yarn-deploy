# kristofvc.webpack_encore_yarn_deploy

A role to install node_modules through yarn and build your assets with webpack-encore

## Requirements

- Yarn should be installed and available where you run this role
- Webpack-encore as a node_module
- A webpack config file

## Installation

Install this role by running `ansible-galaxy install kristofvc.webpack_encore_yarn_deploy` from a command-line.

## Role Variables

All default variables are set in defaults/main.yml, you can overwrite these at will.

```yml
  # yarn install --help
  yarn_options: ""

  # which version of assets to deploy, by default this could be dev, dev-server or production
  encore_environment: "production"

  # options you can define, like --host, --hot, etc. See webpack encore and webpack documentation
  # yarn run encore --help
  # yarn run webpack --help
  encore_options: "--progress --optimize-minimize --verbose"

  # if a cleanup of node_modules should happen
  do_cleanup: true
```

## Example Playbook

Minimal config for a playbook using this role, based on the config for [Ansistrano](https://github.com/ansistrano/deploy) and Cbrunnkvist's [Ansistrano symfony deploy](https://github.com/cbrunnkvist/ansistrano-symfony-deploy).

```yml
---
-
  name: Deploy Application
  hosts: all
  gather_facts: false
  vars:
    # Ansistrano vars
    ansistrano_deploy_to: "<deploy-to-path>"
    ansistrano_deploy_via: "git"
    ansistrano_git_repo: <git-repo>
    ansistrano_git_branch: master
    ansistrano_keep_releases: 3

    # Symfony vars
    symfony_env: prod
    symfony_console_path: 'bin/console'

    # Webpack encore vars
    encore_path: "{{ ansistrano_release_path.stdout }}"
  environment:
    APP_ENV: "prod"

  roles:
    - { role: kristofvc.webpack_encore_yarn_deploy }
```

License
-------

[MIT](https://en.wikipedia.org/wiki/MIT_License)

Author Information
------------------

Written by [Kristof Van Cauwenbergh](https://github.com/kristofvc). Based and build upon the work of [Ansistrano](https://github.com/ansistrano/deploy) and Cbrunnkvist's [Ansistrano symfony deploy](https://github.com/cbrunnkvist/ansistrano-symfony-deploy).

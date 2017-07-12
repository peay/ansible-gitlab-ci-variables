gitlab-ci-variables
===================

This role allows to manage Gitlab CI variables using Ansible.

The role can create or update variable value, and also track
existing Gitlab CI variables that are not specified in the
role configuration.

[![Build Status](https://travis-ci.org/peay/ansible-gitlab-ci-variables.svg?branch=master)](https://travis-ci.org/peay/ansible-gitlab-ci-variables)
[![Ansible Galaxy](https://img.shields.io/badge/ansible-peay.gitlab--ci--variables-blue.svg)](https://galaxy.ansible.com/peay/gitlab-ci-variables/)

Requirements
------------

Gitlab with v4 API (Gitlab 9.0+).

Installation
-------------

```sh
ansible-galaxy install peay.gitlab-ci-variables
```

Usage
-----

Variables are documented in [defaults/main.yml](defaults/main.yml).

API URL and token can be specified via
```yaml
# API token for Gitlab
gitlab_token: "XXXXXXXXXXXXXXXXXXXX"

# API URL for Gitlab
gitlab_api_url: https://some-url-to-gitlab.com/api/v4
```

Gitlab CI variables can be managed per project. The following example
manages variables for two projects.

```yaml
# Variables to manage for each Gitlab project
gitlab_ci_variables:
  - project: "group/project"
    variables:
      - key: VARIABLE_1
        value: value

  - project: "group/project2"
    variables:
      - key: VARIABLE_1
        value: value
      - key: VARIABLE_2
        value: value
```

By default, the role will also check for Gitlab CI variables that
are unknown (i.e., not specified in `gitlab_ci_variables`). This
can be disabled using

```yaml
# When enabled, check for unknown variables in Gitlab
# not managed by this role
gitlab_ci_check_unknown: false
```

This is purely a check. The role will not remove existing variables
that are unknown.

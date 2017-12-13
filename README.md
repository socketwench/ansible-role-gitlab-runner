# Ansible Role: Gitlab Runner

Installs Gitlab Runner and configures runners.

## Requirements

None.

## Using the role

To install the latest version of Gitlab Runner without any additional configuration, just add the role to your playbook:

    roles:
     - socketwench.gitlab-runner

## Role Variables

Available variables are listed below, along with default values (see `defaults/main.yml`).

### Global runner configuration

`gitlab_runner_concurrent_jobs`

Specifies the number of jobs that may run simultaneously. Default: `1`.

`gitlab_runner_log_level`

The log level of the runner system. Default: `error`.

`gitlab_runner_check_interval`

How often to check for new jobs. Default: `0`.

`gitlab_runner_coordinator_url`

The Gitlab CI coordinator URL. You can find this in Gitlab by navigating to a specific project, clicking on **Settings**, then **CI/CD Pipelines**.

### Creating runners

If you want to create runners, define the `gitlab_runners` variable:

    gitlab_runners:
      - name: "my_runner_name"
        token: "1234567890qwertyuiopasdfghjkl"

By default, if you do not specify an `executor`, it will assume `shell`. See the example playbook below for an SSH executor example.

## Dependencies

None.

## Example Playbook

    ---
    - hosts: all
      vars:
        gitlab_runner_coordinator_url: "https://gitlab.example.com/ci"
        gitlab_runners:
          - name: "my_runner_name"
            token: "1234567890qwertyuiopasdfghjkl"
            executor: "ssh"
            ssh_user: "setec_astonomy"
            ssh_password: "toomanysecrets"
            ssh_host: "sneakers.example.com"

      roles:
       - socketwench.gitlab-runner

## License

GPL 3.0.

## Author Information

This role was created in 2017 by [socketwench](https://deninet.com/).

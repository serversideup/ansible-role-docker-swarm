<p align="center">
		<a href="https://github.com/serversideup/ansible-role-docker-swarm"><img src="https://raw.githubusercontent.com/serversideup/ansible-role-docker-swarm/main/.github/img/header.png" width="1280" alt="GitHub Header"></a>
</p>
<p align="center">
	<a href="https://github.com/serversideup/ansible-role-docker-swarm/actions/workflows/publish_docker-images-production.yml"><img alt="Build Status" src="https://img.shields.io/github/actions/workflow/status/serversideup/ansible-role-docker-swarm/release.yml"></a>
	<a href="https://github.com/serversideup/ansible-role-docker-swarm/blob/main/LICENSE" target="_blank"><img src="https://badgen.net/github/license/serversideup/ansible-role-docker-swarm" alt="License"></a>
	<a href="https://github.com/sponsors/serversideup"><img src="https://badgen.net/badge/icon/Support%20Us?label=GitHub%20Sponsors&color=orange" alt="Support us"></a>
  <br />
  <a href="https://community.serversideup.net"><img alt="Discourse users" src="https://img.shields.io/discourse/users?color=blue&server=https%3A%2F%2Fcommunity.serversideup.net"></a>
  <a href="https://serversideup.net/discord"><img alt="Discord" src="https://img.shields.io/discord/910287105714954251?color=blueviolet"></a>
</p>

Hi! We're [Dan](https://twitter.com/danpastori) and [Jay](https://twitter.com/jaydrogers). We're a two person team with a passion for open source products. We created [Server Side Up](https://serversideup.net) to help share what we learn.

### Find us at:

* 📖 [Blog](https://serversideup.net) - get the latest guides and free courses on all things web/mobile development.
* 🙋 [Community](https://community.serversideup.net) - get friendly help from our community members.
* 🤵‍♂️ [Get Professional Help](https://serversideup.net/get-help) - get guaranteed responses within next business day.
* 💻 [GitHub](https://github.com/serversideup) - check out our other open source projects
* 📫 [Newsletter](https://serversideup.net/subscribe) - skip the algorithms and get quality content right to your inbox
* 🐥 [Twitter](https://twitter.com/serversideup) - you can also follow [Dan](https://twitter.com/danpastori) and [Jay](https://twitter.com/jaydrogers)
* ❤️ [Sponsor Us](https://github.com/sponsors/serversideup) - please consider sponsoring us so we can create more helpful resources

### Our Sponsors
All of our software is free an open to the world. None of this can be brought to you without the financial backing of our sponsors.

<p align="center"><a href="https://github.com/sponsors/serversideup"><img src="https://521public.s3.amazonaws.com/serversideup/sponsors/sponsor-box.png" alt="Sponsors"></a></p>

#### Individual Supporters
<!-- supporters --><a href="https://github.com/alexjustesen"><img src="https://github.com/alexjustesen.png" width="40px" alt="alexjustesen" /></a>&nbsp;&nbsp;<a href="https://github.com/GeekDougle"><img src="https://github.com/GeekDougle.png" width="40px" alt="GeekDougle" /></a>&nbsp;&nbsp;<!-- supporters -->

Docker Swarm Ansible Role
=========

Deploy and maintain Docker Swarm servers easily. This role was inspired by [Jeff Geerling](https://github.com/geerlingguy), but expanded to support Docker Swarm. Please support his amazing work!

Requirements
------------

For now, this project focuses on supporting **Ubuntu 22.04** only. Choose any host that you'd like. All this role needs is an SSH connection to a user that has `sudo` privileges.

Role Variables
--------------

You can find all variables organized and documented in `defaults/main.yml`. Feel free to override any variable of your choice.

```yml
---
# Edition can be one of: 'ce' (Community Edition) or 'ee' (Enterprise Edition).
docker_edition: 'ce'

# Docker repo URL.
docker_repo_url: https://download.docker.com/linux

# Used only for Debian/Ubuntu. Switch 'stable' to 'nightly' if needed.
docker_apt_release_channel: stable
docker_apt_arch: "{{ 'arm64' if ansible_architecture == 'aarch64' else 'amd64' }}"
docker_apt_repository: "deb [arch={{ docker_apt_arch }} signed-by=/etc/apt/trusted.gpg.d/docker.asc] {{ docker_repo_url }}/{{ ansible_distribution | lower }} {{ ansible_distribution_release }} {{ docker_apt_release_channel }}"
docker_apt_ignore_key_error: true
docker_apt_gpg_key: "{{ docker_repo_url }}/{{ ansible_distribution | lower }}/gpg"
docker_apt_gpg_key_checksum: "sha256:1500c1f56fa9e26b9b8f42452a553675796ade0807cdce11975eb98170b3a570"

# Docker user configuration.
docker_user:
  username: deploy
  uid: 9999
  group: deploy
  secondary_groups: "docker"
  gid: 9999
  ## Uncomment to set authorized SSH keys for the docker user.
  # authorized_ssh_keys: 
  #   - "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIKNJGtd7a4DBHsQi7HGrC5xz0eAEFHZ3Ogh3FEFI2345 fake@key"
  #   - "ssh-ed25519 AAAAC3NzaC1lZDI1NTE5AAAAIFRfXxUZ8q9vHRcQZ6tLb0KwGHu8xjQHfYopZKLmnopQ anotherfake@key"
```

Dependencies
------------
See [`requirements.yml`](./requirements.yml) for all collection dependencies.

To install all dependencies, run:

```bash
ansible-galaxy install -r requirements.yml
```

Example Playbook
----------------

Including an example of how to use your role (for instance, with variables passed in as parameters) is always nice for users too:

```yml
    - hosts: servers
      roles:
         - role: serversideup.docker_swarm
```

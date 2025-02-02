**One Identity open source projects are supported through [One Identity GitHub issues](https://github.com/OneIdentity/ars-ps/issues) and the [One Identity Community](https://www.oneidentity.com/community/). This includes all scripts, plugins, SDKs, modules, code snippets or other solutions. For assistance with any One Identity GitHub project, please raise a new Issue on the [One Identity GitHub project](https://github.com/OneIdentity/ars-ps/issues) page. You may also visit the [One Identity Community](https://www.oneidentity.com/community/) to ask questions.  Requests for assistance made through official One Identity Support will be referred back to GitHub and the One Identity Community forums where those requests can benefit all users.**

# Safeguard Authentication Services Ansible Collection

The One Identity Safeguard Authentication Services Ansible Collection, referred to as `ansible-authentication-services`, consists of roles, modules, plugins, report templates, and sample playbooks to automate software deployment, configuration, Active Directory joining, profiling, and report generation for [Safeguard Authentication Services](https://www.oneidentity.com/products/authentication-services/). 

## Collection Contents

* [`common role`](roles/common/README.md): Common tasks and variables required by other roles.

* [`client_preflight role`](roles/client_preflight/README.md): Check client readiness for software install and AD join.
    * [`preflight module`](roles/client_preflight/README.md#plugins) Performs preflight tasks on host.

* [`client_sw role`](roles/client_sw/README.md): Client software install, upgrade, downgrade, uninstall, and version checking.
    * [`client_sw_pkgs module`](roles/client_sw/README.md#plugins) Client software install package directory checking.
    * [`pkgdict2items filter`](roles/client_sw/README.md#plugins) Client software package sorting by state and name.

* [`client_join role`](roles/client_join/README.md): Client Active Directory joining/unjoining.
    * [`vastool_join module`](roles/client_join/README.md#plugins) Performs Active Directory join/unjoin tasks on host.

* [`client_config role`](roles/client_config/README.md): Client configuration.
    * [`dictlistselect filter`](roles/client_config/README.md#plugins) Filter list of dicts to only include specified keys.

* [`client_join_status role`](roles/client_join_status/README.md): Checks the Active Directory join status of client hosts.

* [`client_agent_status role`](roles/client_agent_status/README.md): Checks the health status of client agents.
    * [`vastool_status module`](roles/client_agent_status/README.md#plugins) Tests the machine's join against Active Directory and local configuration for various issues.

### Host reports

* [`unix_computers_in_ad role`](roles/unix_computers_in_ad/README.md): Lists all Unix computers in Active Directory in the requested scope.

### User reports

* [`ad_user_conflicts role`](roles/ad_user_conflicts/README.md): Lists all users with Unix User ID numbers (UID numbers) assigned to other Unix-enabled user account.

* [`local_unix_user_conflicts role`](roles/local_unix_user_conflicts/README.md): Identifies local user accounts that would conflict with a specified user name and UID on other hosts.

* [`local_unix_users role`](roles/local_unix_users/README.md): Lists all users on all hosts or lists the hosts where a specific user account exists in /etc/passwd.
    * [`get_local_unix_users module`](roles/local_unix_users/README.md#plugins) Reads, filters and returns data from /etc/passwd.

* [`local_unix_users_with_ad_logon role`](roles/local_unix_users_with_ad_logon/README.md): Identifies the local user accounts that are required to use Active Directory credentials to log onto the Unix hosts.

* [`unix_enabled_ad_users role`](roles/unix_enabled_ad_users/README.md): Lists all Active Directory users that have Unix user attributes.

### Group reports

* [`ad_group_conflicts role`](roles/ad_group_conflicts/README.md): Lists all Active Directory groups with Unix Group ID (GID) numbers assigned to other Unix-enabled groups.

* [`local_unix_groups role`](roles/local_unix_groups/README.md): Lists all groups on all hosts or lists the hosts where a specific group exists in /etc/group.
    * [`get_local_unix_groups module`](roles/local_unix_groups/README.md#plugins) Reads, filters and returns data from /etc/group.

* [`unix_enabled_ad_groups role`](roles/unix_enabled_ad_groups/README.md): Lists all Active Directory groups that have Unix group attributes.

### Access & Privileges reports

* [`logon_policy_for_unix_host role`](roles/logon_policy_for_unix_host/README.md): Identifies the Active Directory users that have been explicitly granted log on permissions for the Unix hosts.

* [`logon_policy_for_ad_user role`](roles/logon_policy_for_ad_user/README.md): Identifies the hosts where Active Directory users have been granted log on permission.

* [`host_access_control role`](roles/host_access_control/README.md): Show the content of users.allow and users.deny files.
    * [`get_host_access_control module`](roles/host_access_control/README.md#plugins) Reads and returns data from users.allow and users.deny.

## Installation

### Prerequisites

* [Ansible](https://github.com/ansible/ansible) version 2.9 or later

    * `Collections are a new feature introduced in Ansible version 2.9.  Please use the latest 2.9+ release for the best user experience.`

* [Jinja](https://github.com/pallets/jinja) version 2.10 or later.

* One Identity [Safeguard Authentication Services](https://www.oneidentity.com/products/authentication-services/) version 4.2.x or later

    * `This collection expects the components and structure of Safeguard Authentication Services 4.2.x or later.`
    * See collection role [documentation](docs/) for specific, per-role  requirements and instructions.
    * See One Identity [Safeguard Authentication Services documentation](https://support.oneidentity.com/authentication-services/4.2.4/technical-documents) for requirements and instructions.

### From Ansible Galaxy 

To install from [Ansible Galaxy](https://galaxy.ansible.com/) you can use the [ansible-galaxy](https://docs.ansible.com/ansible/latest/cli/ansible-galaxy.html) command to install the collection on your control node.  See [Ansible documentation](https://docs.ansible.com/ansible/devel/user_guide/collections_using.html#installing-collections) for futher information.

Using `ansible-galaxy` command:
```bash
ansible-galaxy collection install oneidentity.authentication_services
```

The collection can also be added to a project's `requirements.yml` file
```yaml
---
collections:
  - name: oneidentity.authentication_services
```

and installed using the `ansible-galaxy` command.  This method allows all required collections for a project to be specified in one place and installed with one command.
```bash
ansible-galaxy collection install -r requirements.yml
```

When used with [Ansible Tower](https://www.ansible.com/products/tower) and [Ansible AWX](https://github.com/ansible/awx) the collections in the project's `requirements.yml` file are automatically installed each time a project is run and there is no need to use the `ansible-galaxy` command.

### From GitHub

For the examples in this section please see `ansible-authentication-services` [releases page](https://github.com/OneIdentity/ansible-authentication-services/releases) to find the latest collection build artifact (*.tar.gz file) and use the URL to this file in place of the URL's shown below.  The collection build artifact is under the 'Assets' section for each release (right click on the *.tar.gz file and select 'Copy link address' to copy URL).

To install from [GitHub](https://github.com/OneIdentity/ansible-authentication-services) you can use the [ansible-galaxy](https://docs.ansible.com/ansible/latest/cli/ansible-galaxy.html) command to install the collection on your control node.  See [Ansible documentation](https://docs.ansible.com/ansible/devel/user_guide/collections_using.html#installing-collections) for futher information.

Using `ansible-galaxy` command:
```bash
ansible-galaxy collection install https://github.com/OneIdentity/ansible-authentication-services/releases/download/v0.2.3/oneidentity-authentication_services-0.2.3.tar.gz
```

The collection can also be added to a project's `requirements.yml` file
```yaml
---
collections:
  - name: https://github.com/OneIdentity/ansible-authentication-services/releases/download/v0.2.3/oneidentity-authentication_services-0.2.3.tar.gz
```

and installed using the `ansible-galaxy` command.  This method allows all required collections for a project to be specified in one place and installed with one command.
```bash
ansible-galaxy collection install -r requirements.yml
```

When used with [Ansible Tower](https://www.ansible.com/products/tower) and [Ansible AWX](https://github.com/ansible/awx) the collections in the project's `requirements.yml` file are automatically installed each time a project is run and there is no need to use the `ansible-galaxy` command.

### Local Build and Install

For local build and installation, you can clone the Git repository, build the collection artifact, and install the locally built collection artifact.  This would be useful for those wishing to extend or customize the collection.

1. Clone the Git repository:

    ```bash
    git clone https://github.com/OneIdentity/ansible-authentication-services.git
    ```

2. Run a local build inside the collection using the [ansible-galaxy](https://docs.ansible.com/ansible/latest/cli/ansible-galaxy.html) command in the root directory of the cloned repository:

    ```bash
    cd ansible-authentication-services
    ansible-galaxy collection build
    ```

    The build command will generate an Ansible Galaxy collection artifact with a `tar.gz` file extension, sample output will look like the following:

    ```
    Created collection for oneidentity.authentication_services at /home/user/ansible-authentication-services/oneidentity-authentication_services-0.2.3.tar.gz
    ```

    `Pleae note the path shown above is just an example, the path to your build artifact will be in the root directory of the cloned repository.`

3. Install the locally-built collection artifact using the [ansible-galaxy](https://docs.ansible.com/ansible/latest/cli/ansible-galaxy.html) command to install the collection on your control node.  See [Ansible documentation](https://docs.ansible.com/ansible/devel/user_guide/collections_using.html#installing-collections) for futher information.

    Using `ansible-galaxy` command:

    ```bash
    ansible-galaxy collection install /home/user/ansible-authentication-services/oneidentity-authentication_services-0.2.3.tar.gz
    ```

    The collection can also be added to a project's `requirements.yml` file
    ```yaml
    ---
    collections:
    - name: /home/user/ansible-authentication-services/oneidentity-authentication_services-0.2.3.tar.gz
    ```

    and installed using the `ansible-galaxy` command.  This method allows all required collections for a project to be specified in one place and installed with one command.
    ```bash
    ansible-galaxy collection install -r requirements.yml
    ```

When used with [Ansible Tower](https://www.ansible.com/products/tower) and [Ansible AWX](https://github.com/ansible/awx) the collections in the project's `requirements.yml` file are automatically installed each time a project is run and there is no need to use the `ansible-galaxy` command.

## Usage

The collection provides various sample playbooks in the [examples](examples/README.md) directory. 

## Supported Platforms

All [Safeguard Authentication Services supported platforms](https://support.oneidentity.com/technical-documents/authentication-services/4.2.4/release-notes/2#TOPIC-1376245).

## Notes

### Known issues

* Check mode does not work as expected for the client_sw role.  No changes are made and it doesn't cause errors but the stated changes that would or would not be made if run normally are not accurate.
* The directory of client software install packages has to be on the Ansible control node.  It would be nice to be able to point to this directory on another machine but this is not possible at this time.
* The IPV4 address for HP-UX machines does not show up in the CSV and HTML reports, this is due to differences in how facts are reported for this OS.  No plan to fix this issue at this time.

### TODO's

* Implement client_profile role.
* Other roles/features depending on interest may include roles to automate server software deployment, server configuration, and server profiling.

# Delphix Target Host

[![Chef cookbook](https://img.shields.io/cookbook/v/delphix.svg)](https://supermarket.chef.io/cookbooks/delphix)

Configure a Linux system as a target host for the Delphix platform.

#### Table of Contents
1.  [Description](#description)
2.  [Installation](#installation)
3.  [Usage](#usage)
4.  [Contribute](#contribute)
    *   [Code of conduct](#code-of-conduct)
    *   [Community Guidelines](#community-guidelines)
    *   [Contributor Agreement](#contributor-agreement)
5.  [Reporting Issues](#reporting-issues)
6.  [Statement of Support](#statement-of-support)
7.  [License](#license)

## <a id="description"></a>Description

This cookbook will configure a Linux system for use as a target host in the Delphix platform. This includes installing all required packages, and creating a `delphix` user with sufficient sudo privileges support all platform operations, most notably managing NFS mounts.  The resulting host can be used with a standard username, directories, and SSH key access.

## <a id="installation"></a>Installation

Berkshelf:<br />
`cookbook 'delphix', '~> 0.1.2'`

Policyfile:<br />
`cookbook 'delphix', '~> 0.1.2', :supermarket`

Knife:<br />
`knife cookbook site install delphix`<br />
`knife cookbook site download delphix`

## <a id="usage"></a>Usage

The cookbook provides a mechanism for configuring the `delphix` user with a single engine public SSH key in `/home/delphix/.ssh/authorized_keys`. In the event that you are building a cloud image and want to configure the SSH key at runtime, you can use cloud init (as described for AWS [here](https://docs.aws.amazon.com/AWSEC2/latest/UserGuide/user-data.html)) to append one or more SSH keys to the `authorized_keys` file on first boot. To get the public SSH key of an engine, use the `system get sshPublicKey` CLI command.

The Delphix cookbook can configure the target host automatically with default settings. If you want to set up a target host quickly, apply the following manifest:

```
delphix::default
```
In the event that your target host needs to have a different user:group than `delphix` or different mount and toolkit directories, chnage the following default attributes to fit your situation.

```
default['delphix']['user'] = 'delphix'
default['delphix']['group'] = 'delphix'
default['delphix']['mount'] = "/mnt/#{default['delphix']['user']}"
default['delphix']['toolkit'] = "/home/#{default['delphix']['user']}/toolkit"
default['delphix']['ssh']['user'] = 'delphix'
default['delphix']['ssh']['key'] = 'AAAAB3Nza[...]qXfdaQ=='
```

The delphix cookbook configures a target host by default, but if you only want to configure a target host it can be called directly:

```
delphix::config_targethost
```

#### Limitations

This cookbook has been manually tested against latest Ubuntu and CentOS AMIs, but there is no reason it should not work with any RedHat or Debian variant.

## <a id="contribute"></a>Contribute

1.  Fork the project.
2.  Make your bug fix or new feature.
3.  Add tests for your code.
4.  Send a pull request.

Contributions must be signed as `User Name <user@email.com>`. Make sure to [set up Git with user name and email address](https://git-scm.com/book/en/v2/Getting-Started-First-Time-Git-Setup). Bug fixes should branch from the current stable branch. New features should be based on the `master` branch.

#### <a id="code-of-conduct"></a>Code of Conduct

This project operates under the [Delphix Code of Conduct](https://delphix.github.io/code-of-conduct.html). By participating in this project you agree to abide by its terms.

#### <a id="contributor-agreement"></a>Contributor Agreement

All contributors are required to sign the Delphix Contributor agreement prior to contributing code to an open source repository. This process is handled automatically by [cla-assistant](https://cla-assistant.io/). Simply open a pull request and a bot will automatically check to see if you have signed the latest agreement. If not, you will be prompted to do so as part of the pull request process.

## <a id="reporting_issues"></a>Reporting Issues

Issues should be reported in the GitHub repo's issue tab. Include a link to it.

## <a id="statement-of-support"></a>Statement of Support

This software is provided as-is, without warranty of any kind or commercial support through Delphix. See the associated license for additional details. Questions, issues, feature requests, and contributions should be directed to the community as outlined in the [Delphix Community Guidelines](https://delphix.github.io/community-guidelines.html).

## <a id="license"></a>License

This is code is licensed under the Apache License 2.0. Full license is available [here](./LICENSE).

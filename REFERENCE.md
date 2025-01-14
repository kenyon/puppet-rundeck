# Reference

<!-- DO NOT EDIT: This document was generated by Puppet Strings -->

## Table of Contents

### Classes

#### Public Classes

* [`rundeck`](#rundeck): Class to manage installation and configuration of Rundeck.

#### Private Classes

* `rundeck::config`: This class is called from rundeck to manage the configuration.
* `rundeck::config::framework`: This private class is called from rundeck::config used to manage the framework properties of rundeck.
* `rundeck::config::jaas_auth`: This private class is called from rundeck::config used to manage jaas authentication for rundeck.
* `rundeck::config::ssl`: This private class is called from rundeck::config used to manage the ssl properties if ssl is enabled.
* `rundeck::install`: This class is called from rundeck for install.
* `rundeck::service`: This class is called from rundeck to manage service.

### Defined types

* [`rundeck::config::aclpolicyfile`](#rundeck--config--aclpolicyfile): This define will create a custom acl policy file.
* [`rundeck::config::plugin`](#rundeck--config--plugin): This define will install a rundeck plugin.

### Functions

* [`validate_rd_policy`](#validate_rd_policy): ''

### Data types

* [`Rundeck::Auth_config`](#Rundeck--Auth_config): Rundeck authentication config type.
* [`Rundeck::Db_config`](#Rundeck--Db_config): Rundeck database config type.
* [`Rundeck::Key_storage_config`](#Rundeck--Key_storage_config): Rundeck key storage config type.
* [`Rundeck::Loglevel`](#Rundeck--Loglevel): Rundeck log level type.
* [`Rundeck::Mail_config`](#Rundeck--Mail_config): Rundeck mail config type.

## Classes

### <a name="rundeck"></a>`rundeck`

Class to manage installation and configuration of Rundeck.

#### Parameters

The following parameters are available in the `rundeck` class:

* [`manage_repo`](#-rundeck--manage_repo)
* [`repo_config`](#-rundeck--repo_config)
* [`package_ensure`](#-rundeck--package_ensure)
* [`manage_home`](#-rundeck--manage_home)
* [`user`](#-rundeck--user)
* [`group`](#-rundeck--group)
* [`manage_user`](#-rundeck--manage_user)
* [`manage_group`](#-rundeck--manage_group)
* [`user_id`](#-rundeck--user_id)
* [`group_id`](#-rundeck--group_id)
* [`admin_policies`](#-rundeck--admin_policies)
* [`api_policies`](#-rundeck--api_policies)
* [`manage_default_admin_policy`](#-rundeck--manage_default_admin_policy)
* [`manage_default_api_policy`](#-rundeck--manage_default_api_policy)
* [`grails_server_url`](#-rundeck--grails_server_url)
* [`clustermode_enabled`](#-rundeck--clustermode_enabled)
* [`execution_mode`](#-rundeck--execution_mode)
* [`java_home`](#-rundeck--java_home)
* [`jvm_args`](#-rundeck--jvm_args)
* [`quartz_job_threadcount`](#-rundeck--quartz_job_threadcount)
* [`auth_config`](#-rundeck--auth_config)
* [`database_config`](#-rundeck--database_config)
* [`framework_config`](#-rundeck--framework_config)
* [`gui_config`](#-rundeck--gui_config)
* [`mail_config`](#-rundeck--mail_config)
* [`security_config`](#-rundeck--security_config)
* [`preauthenticated_config`](#-rundeck--preauthenticated_config)
* [`key_storage_config`](#-rundeck--key_storage_config)
* [`key_storage_encrypt_config`](#-rundeck--key_storage_encrypt_config)
* [`app_log_level`](#-rundeck--app_log_level)
* [`audit_log_level`](#-rundeck--audit_log_level)
* [`config_template`](#-rundeck--config_template)
* [`override_template`](#-rundeck--override_template)
* [`realm_template`](#-rundeck--realm_template)
* [`log_properties_template`](#-rundeck--log_properties_template)
* [`rss_enabled`](#-rundeck--rss_enabled)
* [`server_web_context`](#-rundeck--server_web_context)
* [`ssl_enabled`](#-rundeck--ssl_enabled)
* [`ssl_port`](#-rundeck--ssl_port)
* [`ssl_certificate`](#-rundeck--ssl_certificate)
* [`ssl_private_key`](#-rundeck--ssl_private_key)
* [`key_password`](#-rundeck--key_password)
* [`keystore`](#-rundeck--keystore)
* [`keystore_password`](#-rundeck--keystore_password)
* [`truststore`](#-rundeck--truststore)
* [`truststore_password`](#-rundeck--truststore_password)
* [`service_name`](#-rundeck--service_name)
* [`service_ensure`](#-rundeck--service_ensure)
* [`service_logs_dir`](#-rundeck--service_logs_dir)
* [`service_notify`](#-rundeck--service_notify)
* [`service_config`](#-rundeck--service_config)
* [`service_script`](#-rundeck--service_script)
* [`override_dir`](#-rundeck--override_dir)
* [`api_token_max_duration`](#-rundeck--api_token_max_duration)

##### <a name="-rundeck--manage_repo"></a>`manage_repo`

Data type: `Boolean`

Whether to manage the package repository.

Default value: `true`

##### <a name="-rundeck--repo_config"></a>`repo_config`

Data type: `Hash`

A hash of repository attributes for configuring the rundeck package repositories.
Examples/defaults for yumrepo can be found at RedHat.yaml, and for apt at Debian.yaml

##### <a name="-rundeck--package_ensure"></a>`package_ensure`

Data type: `String[1]`

Ensure the state of the rundeck package, either present, absent or a specific version.

Default value: `'installed'`

##### <a name="-rundeck--manage_home"></a>`manage_home`

Data type: `Boolean`

Whether to manage rundeck home dir.

Default value: `true`

##### <a name="-rundeck--user"></a>`user`

Data type: `String[1]`

The user that rundeck is installed as.

Default value: `'rundeck'`

##### <a name="-rundeck--group"></a>`group`

Data type: `String[1]`

The group permission that rundeck is installed as.

Default value: `'rundeck'`

##### <a name="-rundeck--manage_user"></a>`manage_user`

Data type: `Boolean`

Whether to manage `user` (and enforce `user_id` if set).

Default value: `false`

##### <a name="-rundeck--manage_group"></a>`manage_group`

Data type: `Boolean`

Whether to manage `group` (and enforce `group_id` if set).

Default value: `false`

##### <a name="-rundeck--user_id"></a>`user_id`

Data type: `Optional[Integer]`

If you want to have always the same user id. Eg. because of a NFS share.

Default value: `undef`

##### <a name="-rundeck--group_id"></a>`group_id`

Data type: `Optional[Integer]`

If you want to have always the same group id. Eg. because of a NFS share.

Default value: `undef`

##### <a name="-rundeck--admin_policies"></a>`admin_policies`

Data type: `Array[Hash]`

Admin acl policies.

Default value:

```puppet
[
    {
      'description' => 'Admin, all access',
      'context'     => { 'project' => '.*' },
      'for'         => {
        'resource' => [{ 'allow' => '*' }],
        'adhoc'    => [{ 'allow' => '*' }],
        'job'      => [{ 'allow' => '*' }],
        'node'     => [{ 'allow' => '*' }],
      },
      'by'          => [{ 'group' => ['admin'] }],
    },
    {
      'description' => 'Admin, all access',
      'context'     => { 'application' => 'rundeck' },
      'for'         => {
        'project'  => [{ 'allow' => '*' }],
        'resource' => [{ 'allow' => '*' }],
        'storage'  => [{ 'allow' => '*' }],
      },
      'by'          => [{ 'group' => ['admin'] }],
    },
  ]
```

##### <a name="-rundeck--api_policies"></a>`api_policies`

Data type: `Array[Hash]`

Apitoken acl policies.

Default value:

```puppet
[
    {
      'description' => 'API project level access control',
      'context'     => { 'project' => '.*' },
      'for'         => {
        'resource' => [
          { 'equals' => { 'kind' => 'job' }, 'allow' => ['create', 'delete'] },
          { 'equals' => { 'kind' => 'node' }, 'allow' => ['read', 'create', 'update', 'refresh'] },
          { 'equals' => { 'kind' => 'event' }, 'allow' => ['read', 'create'] },
        ],
        'adhoc'    => [{ 'allow' => ['read', 'run', 'kill'] }],
        'job'      => [{ 'allow' => ['read', 'create', 'update', 'delete', 'run', 'kill'] }],
        'node'     => [{ 'allow' => ['read', 'run'] }],
      },
      'by'          => [{ 'group' => ['api_token_group'] }],
    },
    {
      'description' => 'API Application level access control',
      'context'     => { 'application' => 'rundeck' },
      'for'         => {
        'project'  => [{ 'match' => { 'name' => '.*' }, 'allow' => ['read'] }],
        'resource' => [{ 'equals' => { 'kind' => 'system' }, 'allow' => ['read'] }],
        'storage'  => [{ 'match' => { 'path' => '(keys|keys/.*)' }, 'allow' => '*' }],
      },
      'by'          => [{ 'group' => ['api_token_group'] }],
    },
  ]
```

##### <a name="-rundeck--manage_default_admin_policy"></a>`manage_default_admin_policy`

Data type: `Boolean`

Whether to manage the default admin policy.

Default value: `true`

##### <a name="-rundeck--manage_default_api_policy"></a>`manage_default_api_policy`

Data type: `Boolean`

Whether to manage default api policy.

Default value: `true`

##### <a name="-rundeck--grails_server_url"></a>`grails_server_url`

Data type: `Stdlib::HTTPUrl`

Sets `grails.serverURL` so that Rundeck knows its external address.

Default value: `"http://${facts['networking']['fqdn']}:4440"`

##### <a name="-rundeck--clustermode_enabled"></a>`clustermode_enabled`

Data type: `Boolean`

Wheter to enable cluster mode.

Default value: `false`

##### <a name="-rundeck--execution_mode"></a>`execution_mode`

Data type: `Enum['active', 'passive']`

Set the execution mode to 'active' or 'passive'.

Default value: `'active'`

##### <a name="-rundeck--java_home"></a>`java_home`

Data type: `Optional[Stdlib::Absolutepath]`

Set the home directory of java.

Default value: `undef`

##### <a name="-rundeck--jvm_args"></a>`jvm_args`

Data type: `String`

Extra arguments for the JVM.

Default value: `'-Xmx1024m -Xms256m -server'`

##### <a name="-rundeck--quartz_job_threadcount"></a>`quartz_job_threadcount`

Data type: `Integer`

The maximum number of threads used by Rundeck for concurrent jobs.

Default value: `10`

##### <a name="-rundeck--auth_config"></a>`auth_config`

Data type: `Rundeck::Auth_config`

Hash of properties for configuring [Rundeck JAAS Authentication](https://docs.rundeck.com/docs/administration/security/authentication.html#jetty-and-jaas-authentication)

Default value:

```puppet
{
    'file' => {
      'auth_flag'    => 'required',
      'jaas_config'  => {
        'file' => '/etc/rundeck/realm.properties',
      },
      'realm_config' => {
        'admin_user'     => 'admin',
        'admin_password' => 'admin',
        'auth_users'     => [],
      },
    },
  }
```

##### <a name="-rundeck--database_config"></a>`database_config`

Data type: `Rundeck::Db_config`

Hash of properties for configuring the [Rundeck Database](https://docs.rundeck.com/docs/administration/configuration/database)

Default value: `{ 'url' => 'jdbc:h2:file:/var/lib/rundeck/data/rundeckdb' }`

##### <a name="-rundeck--framework_config"></a>`framework_config`

Data type: `Hash`

Hash of properties for configuring the [Rundeck Framework](https://docs.rundeck.com/docs/administration/configuration/config-file-reference.html#framework-properties)
This hash will be merged with the [Rundeck defaults](https://github.com/voxpupuli/puppet-rundeck/blob/master/manifests/config.pp#L8-L20)

Default value: `{}`

##### <a name="-rundeck--gui_config"></a>`gui_config`

Data type: `Hash`

Hash of properties for customizing the [Rundeck GUI](https://docs.rundeck.com/docs/administration/configuration/gui-customization.html)

Default value: `{}`

##### <a name="-rundeck--mail_config"></a>`mail_config`

Data type: `Rundeck::Mail_config`

A hash of the notification email configuraton.

Default value: `{}`

##### <a name="-rundeck--security_config"></a>`security_config`

Data type: `Hash`

A hash of the rundeck security configuration.

Default value: `{}`

##### <a name="-rundeck--preauthenticated_config"></a>`preauthenticated_config`

Data type: `Hash`

A hash of the rundeck preauthenticated configuration.

Default value: `{}`

##### <a name="-rundeck--key_storage_config"></a>`key_storage_config`

Data type: `Rundeck::Key_storage_config`

An array with hashes of properties for customizing the [Rundeck Key Storage](https://docs.rundeck.com/docs/manual/key-storage/key-storage.html)

Default value: `[{ 'type' => 'db', 'path' => 'keys' }]`

##### <a name="-rundeck--key_storage_encrypt_config"></a>`key_storage_encrypt_config`

Data type: `Array[Hash]`

An array with hashes of properties for customizing the [Rundeck Key Storage converter](https://docs.rundeck.com/docs/administration/configuration/plugins/configuring.html#storage-converter-plugins)

Default value: `[]`

##### <a name="-rundeck--app_log_level"></a>`app_log_level`

Data type: `Rundeck::Loglevel`

The log4j logging level to be set for the Rundeck application.

Default value: `'info'`

##### <a name="-rundeck--audit_log_level"></a>`audit_log_level`

Data type: `Rundeck::Loglevel`

The log4j logging level to be set for the Rundeck autorization.

Default value: `'info'`

##### <a name="-rundeck--config_template"></a>`config_template`

Data type: `String[1]`

The template used for rundeck-config properties. Needs to be in epp format.

Default value: `'rundeck/rundeck-config.properties.epp'`

##### <a name="-rundeck--override_template"></a>`override_template`

Data type: `String[1]`

The template used for rundeck profile overrides. Needs to be in epp format.

Default value: `'rundeck/profile_overrides.epp'`

##### <a name="-rundeck--realm_template"></a>`realm_template`

Data type: `String[1]`

The template used for jaas realm properties. Needs to be in epp format.

Default value: `'rundeck/realm.properties.epp'`

##### <a name="-rundeck--log_properties_template"></a>`log_properties_template`

Data type: `String[1]`

The template used for log properties. Needs to be in epp format.

Default value: `'rundeck/log4j2.properties.epp'`

##### <a name="-rundeck--rss_enabled"></a>`rss_enabled`

Data type: `Boolean`

Boolean value if set to true enables RSS feeds that are public (non-authenticated)

Default value: `false`

##### <a name="-rundeck--server_web_context"></a>`server_web_context`

Data type: `Optional[String[1]]`

Web context path to use, such as "/rundeck". http://host.domain:port/server_web_context

Default value: `undef`

##### <a name="-rundeck--ssl_enabled"></a>`ssl_enabled`

Data type: `Boolean`

Enable ssl for the rundeck web application.

Default value: `false`

##### <a name="-rundeck--ssl_port"></a>`ssl_port`

Data type: `Stdlib::Port`

Ssl port of the rundeck web application.

Default value: `4443`

##### <a name="-rundeck--ssl_certificate"></a>`ssl_certificate`

Data type: `Stdlib::Absolutepath`

Full path to the SSL public key to be used by Rundeck.

Default value: `'/etc/rundeck/ssl/rundeck.crt'`

##### <a name="-rundeck--ssl_private_key"></a>`ssl_private_key`

Data type: `Stdlib::Absolutepath`

Full path to the SSL private key to be used by Rundeck.

Default value: `'/etc/rundeck/ssl/rundeck.key'`

##### <a name="-rundeck--key_password"></a>`key_password`

Data type: `Optional[String[1]]`

The password used to protect the key in keystore.

Default value: `undef`

##### <a name="-rundeck--keystore"></a>`keystore`

Data type: `Stdlib::Absolutepath`

Full path to the java keystore to be used by Rundeck.

Default value: `'/etc/rundeck/ssl/keystore'`

##### <a name="-rundeck--keystore_password"></a>`keystore_password`

Data type: `String[1]`

The password for the given keystore.

Default value: `'adminadmin'`

##### <a name="-rundeck--truststore"></a>`truststore`

Data type: `Stdlib::Absolutepath`

The full path to the java truststore to be used by Rundeck.

Default value: `'/etc/rundeck/ssl/truststore'`

##### <a name="-rundeck--truststore_password"></a>`truststore_password`

Data type: `String[1]`

The password for the given truststore.

Default value: `'adminadmin'`

##### <a name="-rundeck--service_name"></a>`service_name`

Data type: `String[1]`

The name of the rundeck service.

Default value: `'rundeckd'`

##### <a name="-rundeck--service_ensure"></a>`service_ensure`

Data type: `Enum['stopped', 'running']`

State of the rundeck service.

Default value: `'running'`

##### <a name="-rundeck--service_logs_dir"></a>`service_logs_dir`

Data type: `Stdlib::Absolutepath`

The path to the directory to store service related logs.

Default value: `'/var/log/rundeck'`

##### <a name="-rundeck--service_notify"></a>`service_notify`

Data type: `Boolean`

Wheter to notify and restart the rundeck service if config changes.

Default value: `true`

##### <a name="-rundeck--service_config"></a>`service_config`

Data type: `Optional[String[1]]`

Allows you to use your own override template instead to config rundeckd init script.

Default value: `undef`

##### <a name="-rundeck--service_script"></a>`service_script`

Data type: `Optional[String[1]]`

Allows you to use your own override template instead of the default from the package maintainer for rundeckd init script.

Default value: `undef`

##### <a name="-rundeck--override_dir"></a>`override_dir`

Data type: `Stdlib::Absolutepath`



##### <a name="-rundeck--api_token_max_duration"></a>`api_token_max_duration`

Data type: `String[1]`



Default value: `'30d'`

## Defined types

### <a name="rundeck--config--aclpolicyfile"></a>`rundeck::config::aclpolicyfile`

This define will create a custom acl policy file.

#### Examples

##### Admin access.

```puppet
rundeck::config::aclpolicyfile { 'myPolicyFile':
  acl_policies => [
    {
      'description' => 'Admin, all access',
      'context'     => { 'project' => '.*' },
      'for'         => {
        'resource' => [{ 'allow' => '*' }],
        'adhoc'    => [{ 'allow' => '*' }],
        'job'      => [{ 'allow' => '*' }],
        'node'     => [{ 'allow' => '*' }],
      },
      'by'          => [{ 'group' => ['admin'] }],
    },
    {
      'description' => 'Admin, all access',
      'context'     => { 'application' => 'rundeck' },
      'for'         => {
        'project'     => [{ 'allow' => '*' }],
        'resource'    => [{ 'allow' => '*' }],
        'storage'     => [{ 'allow' => '*' }],
      },
      'by'          => [{ 'group' => ['admin'] }],
    },
  ],
}
```

#### Parameters

The following parameters are available in the `rundeck::config::aclpolicyfile` defined type:

* [`acl_policies`](#-rundeck--config--aclpolicyfile--acl_policies)
* [`ensure`](#-rundeck--config--aclpolicyfile--ensure)
* [`owner`](#-rundeck--config--aclpolicyfile--owner)
* [`group`](#-rundeck--config--aclpolicyfile--group)
* [`properties_dir`](#-rundeck--config--aclpolicyfile--properties_dir)

##### <a name="-rundeck--config--aclpolicyfile--acl_policies"></a>`acl_policies`

Data type: `Array[Hash]`

An array of hashes containing acl policies. See example.

##### <a name="-rundeck--config--aclpolicyfile--ensure"></a>`ensure`

Data type: `Enum['present', 'absent']`

Set present or absent to add or remove the acl policy file.

Default value: `'present'`

##### <a name="-rundeck--config--aclpolicyfile--owner"></a>`owner`

Data type: `String[1]`

The user that rundeck is installed as.

Default value: `'rundeck'`

##### <a name="-rundeck--config--aclpolicyfile--group"></a>`group`

Data type: `String[1]`

The group permission that rundeck is installed as.

Default value: `'rundeck'`

##### <a name="-rundeck--config--aclpolicyfile--properties_dir"></a>`properties_dir`

Data type: `Stdlib::Absolutepath`

The rundeck configuration directory.

Default value: `'/etc/rundeck'`

### <a name="rundeck--config--plugin"></a>`rundeck::config::plugin`

This define will install a rundeck plugin.

#### Examples

##### Basic usage.

```puppet
rundeck::config::plugin { 'rundeck-hipchat-plugin-1.0.0.jar':
  source => 'http://search.maven.org/remotecontent?filepath=com/hbakkum/rundeck/plugins/rundeck-hipchat-plugin/1.0.0/rundeck-hipchat-plugin-1.0.0.jar',
}
```

#### Parameters

The following parameters are available in the `rundeck::config::plugin` defined type:

* [`source`](#-rundeck--config--plugin--source)
* [`ensure`](#-rundeck--config--plugin--ensure)
* [`owner`](#-rundeck--config--plugin--owner)
* [`group`](#-rundeck--config--plugin--group)
* [`plugins_dir`](#-rundeck--config--plugin--plugins_dir)
* [`proxy_server`](#-rundeck--config--plugin--proxy_server)

##### <a name="-rundeck--config--plugin--source"></a>`source`

Data type: `String[1]`

The http source or local path from which to get the plugin.

##### <a name="-rundeck--config--plugin--ensure"></a>`ensure`

Data type: `Enum['present', 'absent']`

Set present or absent to add or remove the plugin.

Default value: `'present'`

##### <a name="-rundeck--config--plugin--owner"></a>`owner`

Data type: `String[1]`

The user that rundeck is installed as.

Default value: `'rundeck'`

##### <a name="-rundeck--config--plugin--group"></a>`group`

Data type: `String[1]`

The group permission that rundeck is installed as.

Default value: `'rundeck'`

##### <a name="-rundeck--config--plugin--plugins_dir"></a>`plugins_dir`

Data type: `Stdlib::Absolutepath`

Directory where plugins will be installed.

Default value: `'/var/lib/rundeck/libext'`

##### <a name="-rundeck--config--plugin--proxy_server"></a>`proxy_server`

Data type: `Optional[Stdlib::HTTPUrl]`

Get the plugin trough a proxy server.

Default value: `undef`

## Functions

### <a name="validate_rd_policy"></a>`validate_rd_policy`

Type: Ruby 3.x API

''

#### `validate_rd_policy()`

''

Returns: `Any`

## Data types

### <a name="Rundeck--Auth_config"></a>`Rundeck::Auth_config`

Rundeck authentication config type.

Alias of

```puppet
Struct[{
    Optional['file'] => Hash[String, Any],
    Optional['ldap'] => Hash[String, Any],
    Optional['pam']  => Hash[String, Any],
}]
```

### <a name="Rundeck--Db_config"></a>`Rundeck::Db_config`

Rundeck database config type.

Alias of

```puppet
Struct[{
    'url'                                  => String,
    Optional['driverClassName']            => String,
    Optional['username']                   => String,
    Optional['password']                   => Variant[String[8], Sensitive[String[8]]],
    Optional['dialect']                    => String,
    Optional['properties.validationQuery'] => String,
}]
```

### <a name="Rundeck--Key_storage_config"></a>`Rundeck::Key_storage_config`

Rundeck key storage config type.

Alias of

```puppet
Array[Struct[{
      'type'                       => String,
      'path'                       => String,
      Optional['removePathPrefix'] => Boolean,
      Optional['config']           => Hash,
  }]]
```

### <a name="Rundeck--Loglevel"></a>`Rundeck::Loglevel`

Rundeck log level type.

Alias of `Enum['all', 'debug', 'error', 'fatal', 'info', 'off', 'trace', 'warn']`

### <a name="Rundeck--Mail_config"></a>`Rundeck::Mail_config`

Rundeck mail config type.

Alias of

```puppet
Struct[{
    Optional['host']         => String,
    Optional['port']         => Integer,
    Optional['username']     => String,
    Optional['password']     => Variant[String[8], Sensitive[String[8]]],
    Optional['props']        => Array[Hash],
    Optional['default.from'] => String,
    Optional['default.to']   => String,
    Optional['disabled']     => Boolean,
}]
```


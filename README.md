# Squid Proxy

Set up Squid HTTP proxy server.

Role Variables
--------------

### `squid_acl`

A dictionary where keys are names of ACL rules. Values are dictionaries with two keys: `type` and `args`.

`type` is a string as recognized by Squid, such as *src*, *port*, or *method*.

`args` is a list of argument strings to the said ACL. For example, *src* ACL accepts IP addresses with netmasks, or ranges thereof.

### `squid_http_access`

A dictionary with two keys, *deny* and *allow*, each listing ACLs which, when matched, will trigger respective action. Both arrays represent individual rules. Each rule may be either a single matching condition (string), or multiple ANDed conditions (array of strings).

For example:

    deny:
      - "!safe_ports"
      - [ connect_method, "!ssl_ports" ]

renders two rules:

    http_access deny !safe_ports
    http_access deny connect_method !ssl_ports

### `squid_refresh_patterns`

A list of dictionaries, each describing one pattern. Dictionary keys match arguments for `refresh_pattern` directive:

`refresh_pattern` *`regex`* *`min`* *`lm_factor`* *`max`*

`lm_factor` may be given as an integer with or without percent sign, or as a decimal fraction. For example, all the following are identical:

* 42
* 42%
* .42
* 0.42

### `squid_http_port`, `squid_max_object_size`, and `squid_shutdown_lifetime`

Each variable is copied verbatim into its Squid counterpart, i.e. unit names are required, too.

### `squid_cache_dir`

A dictionary where `type` selects cache format, `path` defines its directory, and `args` configure respective format. Order of `args` members will be preserved.

Example Playbook
----------------

    - name: Squid
      hosts: proxy.example.net
      roles:
        - squid

License
-------

GPLv3

Author Information
------------------

Development Gateway

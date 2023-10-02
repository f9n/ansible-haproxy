# f9n.haproxy

Install haproxy


# Examples

```yaml
- hosts: servers
  roles:
    - role: f9n.haproxy
      vars:
        haproxy_frontends: |
          frontend ft_rabbit
            bind *:5672 name rabbit
            default_backend bk_rabbit

          frontend ft_rabbit-mgmt
            bind *:15672 name rabbit-mgmt
            default_backend bk_rabbit-mgmt

        haproxy_backends: |
          backend bk_rabbit
            option tcp-check
            tcp-check connect
            balance roundrobin
            server tt-prmq-loms001 10.250.221.1:5672 check inter 1s
            server tt-prmq-loms002 10.250.221.2:5672 check inter 1s
            server tt-prmq-loms003 10.250.221.3:5672 check inter 1s

          backend bk_rabbit-mgmt
            option tcp-check
            tcp-check connect
            balance roundrobin
            server tt-prmq-loms001 10.250.221.1:15672 check inter 1s
            server tt-prmq-loms002 10.250.221.2:15672 check inter 1s
            server tt-prmq-loms003 10.250.221.3:15672 check inter 1s
```

```yaml
- hosts: servers
  roles:
    - role: f9n.haproxy
      vars:
        haproxy_installation_method: external
        haproxy_rpm_version: 2.0.7

```

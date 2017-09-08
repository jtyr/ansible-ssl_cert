ssl_cert
========

Ansible role which helps to install SSL certificate.

The configuration of the role is done in such way that it should not be
necessary to change the role for any kind of configuration. All can be
done either by changing role parameters or by declaring completely new
configuration as a variable. That makes this role absolutely
universal. See the examples below for more details.

Please report any issues or send PR.


Usage
-----

```
- name: Example of basic usage of this role
  hosts: all
  vars:
    # SSL files
    ssl_cert_key_file: /etc/nginx/ssl/server.key
    ssl_cert_crt_file: /etc/nginx/ssl/server.crt

    # Owner of the SSL files (nginx:nginx)
    ssl_cert_owner: 995
    ssl_cert_group: 993

    # Handler name of the service using the SSL certs
    # (The handler must exist in some other role)
    ssl_cert_service_handler: Restart Nginx service

    # Bundle KEY and CA into one file
    ssl_cert_key_bundle: yes

    # SSL key
    ssl_cert_key: |
      -----BEGIN PRIVATE KEY-----
      MIIEvAIBADANBgkqhkiG9w0BAQEFAASCBKYwggSiAgEAAoIBAQDv1krATvN14+8R
      ypobYKJZEaqk8OxCm62eIcBEJn9qvmm5wDtegZ9RKy79uGY0vnpHDft4WIhDWLUb
      vnthoGjwaicmq7qPCW/2W8Id3hnNlUc9gzqJpEN8NYcpbdDHVeNoKfgO7dDpLk8V
      NZnA1sDxTM8xIG/Fok7pMnMTFWmjT4eQoA7JemycpTdkt5uRLHUECA5ba+hcIa0m
      QSFrmpPTTNeILZ7hrgdzmfn0/QrgV2iohzkWc9E2DWA8x7GihZfoz44Rt3qx+WCD
      rr1L4nlh/6c4JH/dqOnGUKkjyFAAmH85/He+WGlbU6bcLaowKcDbB/k8tOmo7ljD
      r0abnJIlAgMBAAECggEAGuMIIET5kCbMX086NYWAzcFoQvNrWRBAx3B7MGischgE
      nDlLro2TgbL4oqLweks8RAjyPwyVwg8IxqJ1DH3CJemQmAo6cNya+6BPw69pbx2k
      DeZPQqzyj9MkYuWXuTEMvFmwIGRSvkFdxj/rC65HlQWKWLSNMze95vCr6+DDpfYF
      5GYEysBAqQzLmC7FgxXN0goJ7QsR+29VyPBd3TVeBf6idqIFEhLFxPLVlM9UZSo5
      vkONToyLZfDs2To/A0727JRNYpXTfSkHmPfveuzSx1cmZZw/3VV15T8lZazqztb+
      Jo9J3rrjaTPNN77S2ai770eYjimO70119A7NAwpC5QKBgQD/dV6E0KMqX+qbX4dd
      kSq8Hrq9Zk8Pk5pyejDFrto9pDMb8ux/1GR0pO5K8fGCzLQO6MC7XxSPq2p+uePM
      mSVVv+pB7KxIqR7ZN9CaphmKjHDLW5sAd9S/pwNqd3D6iwden8AVIaAClwvTYa7K
      S1GdIEdbxi12nWCH43iKfXnqiwKBgQDwWHIJDoMqW8JbdG7eJhSTg24AU0MAEeYj
      ErWhi4Iqpqmocbs5vUF+vy3F86Wj3Xf5Ch9bzzXuxQ8Cd/IjNtBGN7JSWdNEm2Pb
      lZ09aasMByTNaNT9BoTIFL4VJStyvJ7+45FJEh5ipuZIXJAi87y7Oz05OYxBJzTZ
      kZ0smaX8DwKBgCrBoT1HklewUBsLRSPS/T0ZQ5YZvpfT06DfdLRRjLOOfQNriEvo
      55tiU4P1tL94tZZdPIzf4Bgfz6ZARLFk3IvaoEHCdB+BNumSXvbTYCkBUoum3G2a
      oOAm+vph3WYByQz8XfDrfNWSJGePzOqM6q8KzQa+R7O3qYV0/CLp13L7AoGAW2PG
      ONtj1L9/b/ceESq5uD3JniYK3APyVnPOzNaXcFBfQsW8Q4BLXz6i0RqMaXrVG8VV
      lzt7bodP5chmMi2tlIWpMNcnFndfySdi2u9LMw+kVtb95hiMdOguPywbEU3Xx2QQ
      4pAZLbn45psL076KjUdBSHkxc7TMy84qzcK+8tECgYAbHfKlBC2lwpoXuuA0oxJg
      g4a/Yk2pLEKVf/7Lj6oG2lxSVd1hMMp8lywli3dUYPQO/hsl2P0CA/Dji/KgDANp
      gnHSMGz/CTkQ2inC+NQhmk7Z9Ex3aIEVZsck/lgUKP6t6pKt6aD1oiVx2s2ULSFG
      eXDLzVQ4wWrWiq2QK90Lkw==
      -----END PRIVATE KEY-----

    # SSL cert passed by a variable
    ssl_cert_crt: "{{ my_nginx_crt }}"

    # CA cert read from a file
    ssl_cert_ca: "{{ lookup('file', 'ca.crt') }}"
  roles:
    - ssl_cert

- name: Example of how to install multiple certs
  hosts: all
  vars:
    # List of certificates to install
    ssl_cert_list:
      # This is the first set of certs
      - key:
          file: /etc/nginx/ssl/server.key
          content: "{{ lookup('file', 'nx_server.key') }}"
          # Owner and group of the key
          owner: 995
          group: 993
          # Customized mode for the key
          mode: 0600
        crt:
          file: /etc/nginx/ssl/server.crt
          content: "{{ lookup('file', 'nx_server.crt') }}"
          owner: 995
          group: 993
        ca:
          file: /etc/nginx/ssl/ca.crt
          content: "{{ lookup('file', 'ca.crt') }}"
          owner: 995
          group: 993
        # Service handler to call when certs change
        # (The handler must exist in some other role)
        service_handler: Restart Nginx service
        # Bundle KEY and CA into one file
        key_bundle: yes
      # This is the second set of certs
      - key:
          file: /etc/elasticsearch/ssl/server.key
          content: "{{ lookup('file', 'es_server2.key') }}"
          # User and group (elasticsearch:elasticsearch)
          owner: 996
          group: 994
        crt:
          file: /etc/elasticsearch/ssl/server.crt
          content: "{{ lookup('file', 'es_server1.crt') }}"
          owner: 996
          group: 994
        ca:
          file: /etc/elasticsearch/ssl/ca.crt
          content: "{{ lookup('file', 'es_ca.crt') }}"
          owner: 996
          group: 994
        service_handler: Restart Elasticsearch service
  roles:
    - ssl_cert
```

Server key and self-signed certificate can be created with this command:

```
$ openssl req -x509 -nodes -days 3650 -newkey rsa:2048 -keyout server.key -out server.crt
```


Role variables
--------------

```
# Cert dir permissions
ssl_cert_dir_owner: "{{ ssl_cert_owner }}"
ssl_cert_dir_group: "{{ ssl_cert_group }}"
ssl_cert_dir_mode: "0755"

# Files permissions for all certs
ssl_cert_owner: root
ssl_cert_group: root
ssl_cert_mode: "0640"

# Files permissions for the SSL key
ssl_cert_key_owner: "{{ ssl_cert_owner }}"
ssl_cert_key_group: "{{ ssl_cert_group }}"
ssl_cert_key_mode: "{{ ssl_cert_mode }}"

# Files permissions for the SSL certificate
ssl_cert_crt_owner: "{{ ssl_cert_owner }}"
ssl_cert_crt_group: "{{ ssl_cert_group }}"
ssl_cert_crt_mode: "{{ ssl_cert_mode }}"

# Files permissions for the CA certificate
ssl_cert_ca_owner: "{{ ssl_cert_owner }}"
ssl_cert_ca_group: "{{ ssl_cert_group }}"
ssl_cert_ca_mode: "{{ ssl_cert_mode }}"

# Server SSL key file location
ssl_cert_key_file: null

# Server SSL key
ssl_cert_key: null

# Server SSL certificate file location
ssl_cert_crt_file: null

# Server SSL certificate
ssl_cert_crt: null

# Server CA certificate file location
ssl_cert_ca_file: null

# Server CA certificate
ssl_cert_ca: null

# Whether to bundle the CA cert into the Server cert
ssl_cert_key_bundle: no

# Whether to install the CA cert even if bundle is enabled
ssl_cert_crt_always: no

# Handler name of the service using the SSL certs
# (The handler must exist in some other role)
ssl_cert_service_handler: null

# Default list of certs to install
ssl_cert_list__default:
  - ca:
      file: "{{ ssl_cert_ca_file }}"
      content: "{{ ssl_cert_ca }}"
      owner: "{{ ssl_cert_ca_owner }}"
      group: "{{ ssl_cert_ca_group }}"
      mode: "{{ ssl_cert_ca_mode }}"
      dir_owner: "{{ ssl_cert_dir_owner }}"
      dir_group: "{{ ssl_cert_dir_group }}"
      dir_mode: "{{ ssl_cert_dir_mode }}"
    crt:
      file: "{{ ssl_cert_crt_file }}"
      content: "{{ ssl_cert_crt }}"
      owner: "{{ ssl_cert_crt_owner }}"
      group: "{{ ssl_cert_crt_group }}"
      mode: "{{ ssl_cert_crt_mode }}"
      dir_owner: "{{ ssl_cert_dir_owner }}"
      dir_group: "{{ ssl_cert_dir_group }}"
      dir_mode: "{{ ssl_cert_dir_mode }}"
    key:
      file: "{{ ssl_cert_key_file }}"
      content: "{{ ssl_cert_key }}"
      owner: "{{ ssl_cert_key_owner }}"
      group: "{{ ssl_cert_key_group }}"
      mode: "{{ ssl_cert_key_mode }}"
      dir_owner: "{{ ssl_cert_dir_owner }}"
      dir_group: "{{ ssl_cert_dir_group }}"
      dir_mode: "{{ ssl_cert_dir_mode }}"
    key_bundle: "{{ ssl_cert_key_bundle }}"
    crt_always: "{{ ssl_cert_crt_always }}"
    service_handler: "{{ ssl_cert_service_handler }}"

# Custom list of certs to install
ssl_cert_list__custom: []

# Final list of certs to install
ssl_cert_list: "{{
  ssl_cert_list__default +
  ssl_cert_list__custom }}"
```


License
-------

MIT


Author
------

Jiri Tyr

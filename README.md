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
    ssl_cert_server_key_file: /etc/nginx/ssl/server.key
    ssl_cert_server_cert_file: /etc/nginx/ssl/server.crt

    # Owner of the SSL files (nginx:nginx)
    ssl_cert_owner_file: 996
    ssl_cert_group_file: 994

    # SSL service name
    ssl_cert_service: nginx

    # SSL key
    ssl_cert_server_key: |
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

    # SSL cert
    ssl_cert_server_cert: |
      -----BEGIN CERTIFICATE-----
      MIIDdTCCAl2gAwIBAgIJAPrE+MQxiWWjMA0GCSqGSIb3DQEBCwUAMFExCzAJBgNV
      BAYTAkFVMRMwEQYDVQQIDApTb21lLVN0YXRlMSEwHwYDVQQKDBhJbnRlcm5ldCBX
      aWRnaXRzIFB0eSBMdGQxCjAIBgNVBAMMASowHhcNMTYxMjA2MDIzODM5WhcNMjYx
      MjA0MDIzODM5WjBRMQswCQYDVQQGEwJBVTETMBEGA1UECAwKU29tZS1TdGF0ZTEh
      MB8GA1UECgwYSW50ZXJuZXQgV2lkZ2l0cyBQdHkgTHRkMQowCAYDVQQDDAEqMIIB
      IjANBgkqhkiG9w0BAQEFAAOCAQ8AMIIBCgKCAQEA79ZKwE7zdePvEcqaG2CiWRGq
      pPDsQputniHARCZ/ar5pucA7XoGfUSsu/bhmNL56Rw37eFiIQ1i1G757YaBo8Gon
      Jqu6jwlv9lvCHd4ZzZVHPYM6iaRDfDWHKW3Qx1XjaCn4Du3Q6S5PFTWZwNbA8UzP
      MSBvxaJO6TJzExVpo0+HkKAOyXpsnKU3ZLebkSx1BAgOW2voXCGtJkEha5qT00zX
      iC2e4a4Hc5n59P0K4FdoqIc5FnPRNg1gPMexooWX6M+OEbd6sflgg669S+J5Yf+n
      OCR/3ajpxlCpI8hQAJh/Ofx3vlhpW1Om3C2qMCnA2wf5PLTpqO5Yw69Gm5ySJQID
      AQABo1AwTjAdBgNVHQ4EFgQUwXyjXqvsg7Qc0y5l78c51EgEheAwHwYDVR0jBBgw
      FoAUwXyjXqvsg7Qc0y5l78c51EgEheAwDAYDVR0TBAUwAwEB/zANBgkqhkiG9w0B
      AQsFAAOCAQEAw0fYtICog0V+o9iksaom1QI596DtH2aMz0JAPEABSNujoSDHvNcp
      BL/yjvwLB4JtQgyaKNYh6IqYwvuFWvXtLVeGmVfsAfFL46zcZsL4nT1CYUrmWkno
      oiZk7uMrAEUDSyRbGU6CJZt894qmzIQU1k4js8mTmIFiw7Aiox14vLZsyWQvDXwE
      pR8K0M9uPRuti1b5Uzt78rk6jM1ZQ0WR+BRk7/GAq2lvmJ1RMmOWiwiCiIshHFab
      pj4g/KZwZfkjJOX7jTDcHdULyQa6DIy/kSCYFEBak0jT0nixK1MgtCppOW0CQPvn
      XDqp9AQ3rKf2EIc6ZWZvKHL+A39849xGDA==
      -----END CERTIFICATE-----
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
# Cert files permissions
ssl_cert_owner_file: root
ssl_cert_group_file: root
ssl_cert_mode_file: 0640

# Cert dir permissions
ssl_cert_owner_dir: "{{ ssl_cert_owner_file }}"
ssl_cert_group_dir: "{{ ssl_cert_group_file }}"
ssl_cert_mode_dir: 0755

# Server SSL key file location
ssl_cert_server_key_file: null

# Server SSL key
ssl_cert_server_key: null

# Server SSL certificate file location
ssl_cert_server_cert_file: null

# Server SSL certificate
ssl_cert_server_cert: null

# Server SSL key file location
ssl_cert_ca_cert_file: null

# Server SSL key
ssl_cert_ca_cert: null

# Whether to bundle the CA cert into the Server cert
ssl_cert_server_cert_bundle: no

# Name of the SSL service (e.g. nginx)
ssl_cert_service: null

# Whether to restart the SSL service
ssl_cert_service_restart: yes
```


License
-------

MIT


Author
------

Jiri Tyr

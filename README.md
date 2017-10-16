# ansible-role-resolver

Configures `/etc/resolv.conf`.

If DHCP client is running on the host, this role should not be used. Use
[ansible-role-dhclient](https://github.com/reallyenglish/ansible-role-dhclient)
instead.

## predictable_shuffle filter

`predictable_shuffle` shuffles a list, generates predictably shuffled list
given strings.

```
{{ list_of_ip_address | predictable_shuffle(ansible_fqdn) | list }}
```

# Requirements

None

# Role Variables

| Variable | Description | Default |
|----------|-------------|---------|
| `resolver_nameservers` | list of resolvers | `[]` |
| `resolver_options`     | list of options   | `[]` |

# Dependencies

None

# Example Playbook

```yaml
- hosts: localhost
  roles:
    - ansible-role-resolver
  vars:
    nameservers:
      - 192.168.1.1
      - 192.168.1.2
      - 192.168.1.3
    resolver_nameservers: "{{ nameservers | predictable_shuffle(ansible_fqdn) | list }}"
    resolver_options:
      - timeout:1
      - attempts:1
      - rotate
```

# License

```
Copyright (c) 2016 Tomoyuki Sakurai <tomoyukis@reallyenglish.com>

Permission to use, copy, modify, and distribute this software for any
purpose with or without fee is hereby granted, provided that the above
copyright notice and this permission notice appear in all copies.

THE SOFTWARE IS PROVIDED "AS IS" AND THE AUTHOR DISCLAIMS ALL WARRANTIES
WITH REGARD TO THIS SOFTWARE INCLUDING ALL IMPLIED WARRANTIES OF
MERCHANTABILITY AND FITNESS. IN NO EVENT SHALL THE AUTHOR BE LIABLE FOR
ANY SPECIAL, DIRECT, INDIRECT, OR CONSEQUENTIAL DAMAGES OR ANY DAMAGES
WHATSOEVER RESULTING FROM LOSS OF USE, DATA OR PROFITS, WHETHER IN AN
ACTION OF CONTRACT, NEGLIGENCE OR OTHER TORTIOUS ACTION, ARISING OUT OF
OR IN CONNECTION WITH THE USE OR PERFORMANCE OF THIS SOFTWARE.
```

# Author Information

Tomoyuki Sakurai <tomoyukis@reallyenglish.com>

This README was created by [ansible-role-init](https://gist.github.com/trombik/d01e280f02c78618429e334d8e4995c0)

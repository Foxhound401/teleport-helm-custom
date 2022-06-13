## Roles
A teleport `role` works by having two lists or rules: `allow` rules and `deny` rule. When declaring access rules, keepin in mind the following:
- Everything is denied by default.
- Deny rules get evaluated first and take priority.

A rule consists of two parts: The resources and verbs. Here's an example of an  `allow` rule describing a `list` verb applied to the SSH `sessions` resources.
It means "allow users of this role to see a lit of active SSH sessions".

```yaml
allow:
  - resources: [session]
    verbs: [list]
```

To manage cluster roles, Teleport administrator can use the Web UI or the cli using [tctl resource commands](https://goteleport.com/docs/setup/reference/resources/).
To see the list of roles in a Teleport cluster, an administrator can execute:

```
tctl get roles
```



## Role Template

```yaml
kind: role
versin: v5
metadata:
  name: admin
spec:
  allow:
    logins: ['root', 'isadmin']
    node_labels:
      '*': '*'

    kubernetes_groups: ['edit']
    kubernetes_labels:
      '*': '*'
```

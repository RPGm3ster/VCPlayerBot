---
title: npm-token
section: 1
description: Manage your authentication tokens
---

### Synopsis

```bash
npm token list
npm token revoke <id|token>
npm token create [--read-only] [--cidr=list]
```

Note: This command is unaware of workspaces.

### Description

This lets you list, create and revoke authentication tokens.

* `npm token list`:
  Shows a table of all active authentication tokens. You can request
  this as JSON with `--json` or tab-separated values with `--parseable`.

```bash
+--------+---------+------------+----------+----------------+
| id     | token   | created    | read-only | CIDR whitelist |
+--------+---------+------------+----------+----------------+
| 7f3134 | 1fa9ba… | 2017-10-02 | yes      |                |
+--------+---------+------------+----------+----------------+
| c03241 | af7aef… | 2017-10-02 | no       | 192.168.0.1/24 |
+--------+---------+------------+----------+----------------+
| e0cf92 | 3a436a… | 2017-10-02 | no       |                |
+--------+---------+------------+----------+----------------+
| 63eb9d | 74ef35… | 2017-09-28 | no       |                |
+--------+---------+------------+----------+----------------+
| 2daaa8 | cbad5f… | 2017-09-26 | no       |                |
+--------+---------+------------+----------+----------------+
| 68c2fe | 127e51… | 2017-09-23 | no       |                |
+--------+---------+------------+----------+----------------+
| 6334e1 | 1dadd1… | 2017-09-23 | no       |                |
+--------+---------+------------+----------+----------------+
```

* `npm token create [--read-only] [--cidr=<cidr-ranges>]`:
  Create a new authentication token. It can be `--read-only`, or accept
  a list of
  [CIDR](https://en.wikipedia.org/wiki/Classless_Inter-Domain_Routing)
  ranges with which to limit use of this token. This will prompt you for
  your password, and, if you have two-factor authentication enabled, an
  otp.

  Currently, the cli can not generate automation tokens. Please refer to
  the [docs
  website](https://docs.npmjs.com/creating-and-viewing-access-tokens)
  for more information on generating automation tokens.

```bash
+----------------+--------------------------------------+
| token          | a73c9572-f1b9-8983-983d-ba3ac3cc913d |
+----------------+--------------------------------------+
| cidr_whitelist |                                      |
+----------------+--------------------------------------+
| readonly       | false                                |
+----------------+--------------------------------------+
| created        | 2017-10-02T07:52:24.838Z             |
+----------------+--------------------------------------+
```

* `npm token revoke <token|id>`:
  Immediately removes an authentication token from the registry.  You
  will no longer be able to use it.  This can accept both complete
  tokens (such as those you get back from `npm token create`, and those
  found in your `.npmrc`), and ids as seen in the parseable or json
  output of `npm token list`.  This will NOT accept the truncated token
  found in the normal `npm token list` output.

### Configuration

#### `read-only`

* Default: false
* Type: Boolean

This is used to mark a token as unable to publish when configuring limited
access tokens with the `npm token create` command.

#### `cidr`

* Default: null
* Type: null or String (can be set multiple times)

This is a list of CIDR address to be used when configuring limited access
tokens with the `npm token create` command.

#### `registry`

* Default: "https://registry.npmjs.org/"
* Type: URL

The base URL of the npm registry.

#### `otp`

* Default: null
* Type: null or String

This is a one-time password from a two-factor authenticator. It's needed
when publishing or changing package permissions with `npm access`.

If not set, and a registry response fails with a challenge for a one-time
password, npm will prompt on the command line for one.

### See Also

* [npm adduser](/commands/npm-adduser)
* [npm registry](/using-npm/registry)
* [npm config](/commands/npm-config)
* [npmrc](/configuring-npm/npmrc)
* [npm owner](/commands/npm-owner)
* [npm whoami](/commands/npm-whoami)
* [npm profile](/commands/npm-profile)

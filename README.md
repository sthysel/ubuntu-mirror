# Tool to mirror Ubuntu repos

This tool mirrors Ubuntu repositries for use in Cobbler or other alternative local
sources.

## Assumptions

* This tool will be run on a late Ubuntu server (It can be run on any machine that has `debmirror` installed,
  the recipie below needs to be tweeked for that)
* You have ~200G of disk space and bandwith available

## Install

Clone this repo.

You want the system gpg key in ./keyring:

```
$ gpg --no-default-keyring --keyring ./keyring/trustedkeys.gpg --import /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

Now fuxor with mirror.sh to your liking. The knobs that can be tuned are documented in the script.


Run ```mirror.sh```, it will take as long as 200G will take given your bandwith.


The repo structure will end up looking like so:

```
.
├── keyring/
│   ├── .gitignore
│   ├── README.md
│   ├── trustedkeys.gpg
│   └── trustedkeys.gpg~
├── repomirror/
│   ├── dists/
│   │   ├── trusty/
│   │   │   ├── main/
│   │   │   ├── multiverse/
│   │   │   ├── restricted/
│   │   │   └── universe/
│   │   ├── trusty-security/
│   │   │   ├── main/
│   │   │   ├── multiverse/
│   │   │   ├── restricted/
│   │   │   └── universe/
│   │   └── trusty-updates/
│   │       ├── main/
│   │       ├── multiverse/
│   │       ├── restricted/
│   │       └── universe/
│   ├── pool/
│   │   └── main/
│   │       ├── a/
│   │       └── b/
│   ├── .temp/
│   │   ├── dists/
│   │   │   ├── trusty/
│   │   │   ├── trusty-security/
│   │   │   └── trusty-updates/
│   │   └── .tmp/
│   │       └── dists/
│   └── Archive-Update-in-Progress-elim
├── .gitignore
├── mirror.sh*
└── README.md
```

Once the repo has synced you van expose it over http using nginx, apache or the like.


# Resources

* https://help.ubuntu.com/community/Debmirror

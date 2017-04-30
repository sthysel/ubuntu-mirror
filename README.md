# Tool to mirror Ubuntu repos

This tool mirrors Ubuntu repositories for use in Cobbler or other alternative local
sources.

## Assumptions

* This tool will be run on a late Ubuntu server (It can be run on any machine that has `debmirror` installed,
  the recipe below needs to be tweeked for that)
* You have ~200G of disk space and bandwith available per release you want to mirror. Assuming both i686 and amd64 arches.

## Install

Clone this repo.

You want the system gpg key in ./keyring:

```
$ gpg --no-default-keyring --keyring ./keyring/trustedkeys.gpg --import /usr/share/keyrings/ubuntu-archive-keyring.gpg
```

Now fuxor with mirror.sh to your liking. The knobs that can be tuned are documented in the script. 


Run ```mirror.sh```, its going to take a few hours at least, depending on the releases you want and the architectures of those.
So to only get the i386 of Trusty comes to about 120G.


If selecting only Trusty the repo structure will end up looking like so:

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
├── mirror.sh
└── README.md
```

The `dists` directory will have a set of release specific directories, here there is only trusty.

Once the repo has synced you van expose it over http using nginx, apache or the like.


# Resources

* https://help.ubuntu.com/community/Debmirror

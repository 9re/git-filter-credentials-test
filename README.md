git-filter-credentials-test
====
This is a test repository to use [p5-Git-Filter-Credentials](https://github.com/9re/p5-Git-Filter-Credentials) as a git filter to hide credentials from repo.

====
## Usage

* install [p5-Git-Filter-Credentials](https://github.com/9re/p5-Git-Filter-Credentials)
* write [.gitattributes](https://github.com/9re/git-filter-credentials-test/blob/master/.gitattributes) for files which include credentials.
 * you can skip this if you are cloning this repo for testing.
* define git filter git-filter-credentials in your .git/config

```
[filter "git-filter-credentials"]
        clean=git-filter-credentials --unreplace
		smudge=git-filter-credentials
		required
```

* write replacement rule to `<GIT_ROOT>/.git.filter.credentials` like this.

```
<CLIENT_TOKEN>="actual client token"
<CLIENT_SECRET>="actual client secret"
```

* embed credentials to the files. for, this repo, change config.h as following

```c
#ifndef CONFIG_H
#define CONFIG_H

#define CLIENT_TOKEN "actual client token"
#define CLIENT_SECRET "actual client secret"

#endif
```

the filter system uses simple replacement and unreplacement. so be careful, so as not to have inconsistency with the config file `<GIT_ROOT>/.git.filter.credentials`.

* now that setting has done. and your config.h and the commited one has diff in credentials. only your version has credentials and repo's not. and also the diff is not regarded as a diff in git management system.

====

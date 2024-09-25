# gae-go-testing ⚠️ archived

> ⚠️ This repository is no longer maintained and is archived. The Go ecosystem has evolved a lot with regards to how it uses Context, and the App Engine service has also changed a lot in the meantime. It is unlikely that this library would still work today.

---

Fork of [gae-go-testing](https://github.com/tenntenn/gae-go-testing) with a few minor changes:

- renamed for nicer import syntax (that IDEA's Go Plugin won't highlight as an error)
- added +build tags so that it compiles
- simplified install instructions. 

As of GAE 1.7.5, we now keep tags of the repository that are known to
be compatible with each GAE release. If you are not using the latest
GAE release, please use the associated tag.

Installation
------------

Set environment variables :

    $ export APPENGINE_SDK=/path/to/google_appengine
    $ export PATH=$PATH:$APPENGINE_SDK

Before installing this library, you have to install
[appengine SDK](https://developers.google.com/appengine/downloads#Google_App_Engine_SDK_for_Go).
And copy appengine, appengine_internal and goprotobuf as followings :

    $ export APPENGINE_SDK=/path/to/google_appengine
    $ ln -s $APPENGINE_SDK/goroot/src/pkg/appengine
    $ ln -s $APPENGINE_SDK/goroot/src/pkg/appengine_internal


There is some incompatibility when running the dev server like we do. You can fix
this by changing the top of func init():

	c := readConfig(os.Stdin)
	instanceConfig.AppID = string(c.AppId)
	instanceConfig.APIPort = int(*c.ApiPort)
	instanceConfig.VersionID = string(c.VersionId)
	instanceConfig.InstanceID = *c.InstanceId
	instanceConfig.Datacenter = *c.Datacenter

It should be something like, values don't really matter:

	instanceConfig.AppID = "testapp"
	instanceConfig.APIPort = 8000
	instanceConfig.VersionID = "1.7.7"
	instanceConfig.InstanceID = "instanceid"
	instanceConfig.Datacenter = "instanceid"

This change hasn't produced any noticable issues in running the dev server.

This library can be installed as following :

    $ go get github.com/icub3d/appenginetesting


Usage
-----

The
[documentation](http://godoc.org/github.com/icub3d/appenginetesting)
has some basic examples.  You can also find complete test examples
within [gorca](https://github.com/icub3d/gorca)/(*_test.go). Finally,
[context_test.go](https://github.com/icub3d/appenginetesting/blob/master/context_test.go)
and
[recorder_test.go](https://github.com/icub3d/appenginetesting/blob/master/recorder_test.go)
show an example of usage.

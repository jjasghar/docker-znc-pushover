# znc-pushover

This is a Dockerfile to create a ZNC IRC bouncer with built in [Pushover](https://pushover.net/) support.

Run these commands:
```
mkdir ~/.znc
docker build -t="$USER/znc-pushover" .
docker run -d -p 36667:6667 -v $HOME/.znc:/znc-data $USER/znc-pushover
```

The default password for the web interface is `admin/admin`. You connect via `36667` on both IRC and Web interface.

Check that you have "push" as a module. If so, you have successfully loaded the push notification. Set up your "Edit network" for the
network you want to connect to. Take note of the "Network Name" which will be used in the following setup.

Connect to your ZNC via <yourip:36667> with something like `admin:servernickname:<password>` as the server password.

Create a [new application](https://pushover.net/apps/build) on Pushover, take note of the secret token that it gives you. Also on the
main page your username-token should be in the upper right, take note of that too.

When you have connected to your ZNC run the following commands:

```
/msg *push set service pushover
/msg *push set username your-username-token
/msg *push set secret your-secret-token
/msg *push set target your-device-name-if-you-have-multiple
/msg *push send test
/msg *status connect
```

You should now be connected to your favorite IRC server via ZNC, and have push notifications working. :metal:


I'd like to thank [Jim Myhrberg](https://github.com/jimeh), [Ryan Seys](https://github.com/ryanseys), [Matt Hardcastle](https://github.com/MattHardcastle) for the work done on [docker-znc](https://github.com/jimeh/docker-znc). I took it and ran with it to add push notifications.

<!-- deploying Code to devices -->

Now that we have a device or two connected to a {{ $names.company.lower }} application, let's deploy some code and actually start building something.

A nice first project to get your feet wet is a simple [Haskell][haskell] hello world program which will print a `Hello, world!` message to the logs on the dashboard. All the project source code can be found [here][balena-haskell-hello-world-link].

To clone the project, run the following command in a terminal or your preferred git client:

```shell
$ git clone {{ $links.githubProjects }}/balena-haskell-hello-world
```

Once the repo is cloned, change directory into the newly created `balena-haskell-hello-world` directory and add the balena git remote endpoint by running the command `git remote add` shown in
the top-right corner of your application page:

```shell
$ cd balena-haskell-hello-world
$ git remote add balena <USERNAME>@git.{{ $names.domain }}:<USERNAME>/<APPNAME>.git
```
__Note:__ On other git clients there may be an alternative way to add a remote repository.

So now we have set up a reference in our local git repository (the one on our development computer) to the {{ $names.company.lower }} application remote repository. So when we push new changes to this remote repository it will get compiled and built on our servers and deployed to every device in the application fleet.

__Warning:__ The {{ $names.company.lower }} git repository **is not** intended as a code hosting solution, and we cannot guarantee the persistence of data in {{ $names.company.lower }} git remotes.

Now to deploy this code to all device(s) in the application just run the command:
```shell
$ git push balena master
```

If you want to completely replace the source code of the application with a new source tree, you may need to force the push by running `git push balena master --force`, due to how git works.

__Note:__ On your very first push, git may ask you if you would like to add this host to your list of allowed hosts. If the ECDSA key fingerprint matches `SHA256:NfwmqnKId5cx1RWpebbEuuM87bCJbdyhzRnqFES9Nnw`, you are pushing to the right place. Type 'yes' to continue.

You'll know your code has been successfully compiled and built when our
friendly unicorn mascot appears in your terminal:

<img src="/img/common/pushing/success_unicorn_resin_haskell_hello_world.png" width="80%">

This means your code is safely built and stored on our image registry. It should only take about 5 minutes to build your code and subsequent builds will be quicker because of build caching.


Your application will now be downloaded and executed by all the devices you have connected in your application fleet. You may have to wait about 10 minutes for the first push... So time for more tea, but don't worry, all subsequent pushes are much, much faster due to [Docker layer sharing][dockerLayerDocs]. You can see the progress of the device code updates on the device dashboard:

<img src="/img/common/device/device_dashboard_during_update_generic.png" width="80%">

You should now have the hello world program running on your device and see some logs, including the `Hello, world!` message, on your dashboard.

[balena-haskell-hello-world-link]:{{ $links.githubProjects }}/balena-haskell-hello-world
[dockerLayerDocs]:https://docs.docker.com/engine/userguide/storagedriver/imagesandcontainers/
[haskell]:https://www.haskell.org/

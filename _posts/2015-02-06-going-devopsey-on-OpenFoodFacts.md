---
layout: post
tile: Going DevOpsey on OpenFoodFacts
---

While this is certainly a ropey title, it kind of makes sense since most of the tooling came from the DevOps problematic.
The goal here is to get a repeatable and scriptable way to build from scratch an Open Food Facts server.
Hopefully this is simplify the operation task and allow more people to contribute.

This is not a complicated task, just a bit complex.
I want to make it as simple and easy to reproduce as possible.
That means every step of the way needs to be done with open source tools.
All of the steps also need to be open in order to be improved by the community.
At some point, it all should be part of a CI process somewhere.

My plan is to start by building an image with [packer](https://www.packer.io/).
That will allow us to have a base image to build on top of.
Packer will be used the same way I use to build VM with [the Foreman](http://theforeman.org/).
It requires some information such as:
  * Hardware to be emulated.
  * Where to get the OS iso from.
  * A preseed/kickstart/else to automate the installation process.
  * The type of platform targeted (WMware, VirtualBox, AWS, etc).
  * What configuration management needs running.

Once you created an machine, you can run it with [vagrant](https://www.vagrantup.com/).
It provides a simple way to describe and run an development environments.
You can use different virtualisation providers such as [VirtualBox](http://www.virtualbox.org/), [VMware](http://www.vmware.com/), [Docker](https://www.docker.com/) or [Hyper-V](http://this is not a link to a Microsoft website, no way).
Vagrantfile has lots of similar concept to the packer definition file.
The goal is to do vagrant up and be ready to ssh into the box(es).
Here we only need one box to have the environment ready, for now.

The next step is to get the part that are required to run Open Food Facts &#34;Product Opener&#34; in a package.
It means a package that contain all the requirement (think httpd, mongodb) and the code of OFF itself.
In order to vendorise it all, I plan to use the base image created by packer.
Then I will create a recipe for [fpm-cookery](https://github.com/bernd/fpm-cookery) to build the package.

Finally, once the infrastructure and code requirement are all vendored, I can build a &#34;Product Opener appliance&#34;.
I just to add the package create in the image with packer.                                       

I will post my methodology and advancement here as I go along.                          
Next stop this [github repo](https://github.com/tech-angels/packer-templates).

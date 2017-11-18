# Vagrantfile for [pleroma](https://git.pleroma.social/pleroma/pleroma)

## How to use

 1. $ `vagrant up`
 1. $ `vagrant ssh`
 1. $ (In the guest) `sh startup.sh`
 1. Access http://192.168.1.202:4000 (by default)

## Difference with [official installation procedure](https://git.pleroma.social/pleroma/pleroma/wikis/Installing-on-Debian-Based-Distributions)

 * The guest OS IP address is set to '`192.168.1.202`'.  Modify `config.vm.network` as you like.
 * Use user 'vagrant' for convinience.
 * Don't set up https, reverse-proxy, service, and site-specific data.
 * Database password is fixed.

 Needless to say, this is not for production use.

## Licence

CC0

# STAR Commerce Virtual boxes setup
This repository contains YAML files that define minimal VM setup for STAR Commerce project. 

Note: Contents of this repository are intended to be used with 
[multi box vagrant with puppet setup we provide](https://github.com/the-shop/Environments) only.

## Setup
  - Before you run the `up` command, copy file `puphpet/boxes/STARCommerce/hiera/magento2_data.yaml.dist` to 
 `puphpet/boxes/STARCommerce/hiera/magento2_data.yaml` and update contents of copied file. Magento connect data is 
 mandatory in order to get `magento2` box up and running. Instructions are available here: 
  ([magento connect credentials](https://www.magentocommerce.com/magento-connect/customerdata/secureKeys/list/))
  - Hosts setup: append `192.168.56.100 star.commerce.dev` and `192.168.56.102 magento2.api.provider` lines to your 
  [hosts file](https://en.wikipedia.org/wiki/Hosts_(file)#Location_in_the_file_system). Database can be accessed at 
  `192.168.56.101`, and direct access to app box is on `192.168.56.103`
  - Load Balancer statistics can be accessed at `http://star.commerce.dev/haproxy?stats` with username `haproxy` and 
  password `password` - credentials can be changed in `puphpet/boxes/STARCommerce/hiera/loadbalancer.yaml` file.
  - STAR Commerce application will be accessible through load balancer at 
  [http://star.commerce.dev](http://star.commerce.dev) and Magento 2 installation at 
  [http://magento2.api.provider](http://magento2.api.provider).

## Tweaking resources
This pre-defined setup is intended for development machines with quad core CPUs and at least 8 GB of RAM. If you have 
more than that, feel free to bump up numbers defined in `puphpet/boxes/*.yaml` files (`memory` and `cpus` fields)

## Adding boxes
Adding boxes is as simple as adding a new YAML file to root directory. Make sure there are no collisions in 
names, hostnames, VM names and IPs and you should be good to go.

If you wish to add STAR Commerce frontend box to load balancer rotation, you'll need to modify 
`puphpet/boxes/STARCommerce/hiera/loadbalancer_data.yaml`. If you wish to add load balancing in front of anything else, 
you'll need to create new load balancer box with own setup.

When adding load balancers, it's important that hostname matches `/^*loadbalancer$/` regex.

## IMPORTANT
**For now, this is intended for local setup only, there might be security implications if used on production 
so please DO NOT USE THIS ON PRODUCTION.**
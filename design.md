* why we need etcd if the instances' configurations are already saved elsewhere?
  * we have to know what the currently configuration is. maybe there is someone
  calls configuration API and leave, then how do you know collector configuration's
  current state? By querying the leaved someone? where do you find him? collector may
  deploy at many places and their configuration file are thus scattered, we save configuration
  in etcd so we can use its API to get a current state of the collector system easily.

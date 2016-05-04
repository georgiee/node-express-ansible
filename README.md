# Node Express running on a Vagrant Ubuntu box

## Requirements
+ Vagrant
+ Vagrant Hostmanaer (vagrant plugin install vagrant-hostmanager)
+ Ansible 2.x

Go to folder vagrant and run
`vagrant up`
wait and you should be a running instance of the app in ./web 
on the domain node.dev

The app is mounted from you local filesystem, so you can work in folder ./web
It's running with PM2 in watch mode so the app reloads itself after changing

### Notes file watching, PM2, forever & nodemon
File watchin in PM2 is managed with chokidar. Watching is broken on NFS mounts (related to our symlinks)
so chokidar is forced to use polling.
Forever also supports watching (`-w'), but has no polling fallback
Nodemon also supports watching through chokidar with polling. But let's use PM2 as this app is going to be productive later with PM2.
# vim-arsync :octopus:
vim plugin for asynchronous synchronisation of remote files and local files using rsync

## Main features
- sync up or down project folder using rsync (with compression options etc. -> -avzhe ssh )
- ignore certains files or folder based on configuration file
- asynchronous operation
- project based configuration file
- auto sync up on file save

## Installation
### Dependencies
- rsync
- *vim8* or *neovim*


### Using vim-plug
Place this in your .vimrc:

    Plug 'kenn7/vim-arsync'

... then run the following in Vim:

    :source %
    :PlugInstall
    
    
### Configuration
Create a ```.vim-arsync``` file on the root of your project that contains the following:

```
remote_host     example.com
remote_user    john
remote_passwd  secret 
remote_path     ~/temp/
local_path    /home/ken/temp/vuetest/
ignore_path     ["build/","test/"]
ignore_dotfiles 1
auto_sync_up    0
```

Required fields are:
- ```remote_host```     remote host to connect (must have ssh enabled)
- ```remote_path```     remote folder to be synced

Optional fields are:
- ```remote_user```    username to connect with
- ```remote_passwd```  password to connect with 
- ```local_path```     local folder to be synced (defaults to folder of .vim-arsync)
- ```ignore_path```    list of ingored files/folders
- ```ignore_dotfiles``` set to 1 to not sync dotfiles (e.g. .vim-arsync)
- ```auto_sync_up```   set to 1 for activating automatic upload syncing on file save

NB: fields can be commented out with ```#```
    
## Usage
If ```auto_sync_up``` is set to 1, the plugin will automatically launch the ```:ARsyncUP``` command
everytime a buffer is saved.

### Commands

- ```:ARshowConf``` shows detected configuration
- ```:ARsyncUp``` Syncs files up to the remote (upload local to remote)
- ```:ARsyncDown``` Syncs files down from the remote (download remote to local)

Commands can be mapped to keyboard shortcuts enhance operations

## TODO

- [ ] run more tests
- [ ] handle -u (update) feature of rsync ?
- [ ] deactivate auto sync on error
- [ ] better handle comments in conf file

## Acknoledgements

This plugin was inspired by [vim-hsftp](https://github.com/hesselbom/vim-hsftp) but vim-arsync offers more (rsync, ignore, async...).

This plugins ships with the [async.vim](https://github.com/prabirshrestha/async.vim) library for async operation with vim and neovim.

# Homestead Set-up for Windows 10

### Reference Links:
- https://github.com/eveseat/docs/blob/master/docs/developer_guides/developer_installation.md
- https://laravel.com/docs/6.x/homestead
- https://support.apple.com/kb/DL999?viewlocale=en_US&locale=en_US

### Initial Setup:

1. Choose a virtualization provider (VMWare, VirtualBox, Parallels, etc). I chose VirtualBox, any version later than 6 should do. 
2. Install [Vagrant](https://www.vagrantup.com/downloads.html)

3. Install Homestead. Make a directory in your user file *`C:/Users/*YOUR_USER*/`* named 'Homestead', and clone the git repository:

        git clone https://github.com/laravel/homestead.git ~/Homestead

4. `cd` into the newly created Homestead file and execute `bash init.sh`. This will create your Homestead configuration file, `Homestead.yaml`.

### Configuring Homestead

1. Set your virtualization provider:
`provider: virtualbox`
2. Map the eveseat repo to a shared folder:  
    
        folders:
        - map: c:/path/to/eveseat/repo
        to: /home/vagrant/eveseat

3. Map the shared folder to a site url:

        sites:
        - map: eveseat.test // URL seems to have to be .test to avoid cert issues
        to: /home/vagrant/eveseat/public // the public folder is common for all laravel projects

4. Edit your `c:/windows/System32/drivers/etc/hosts` file to include the IP and site:

        192.168.10.10 homestead.test
        192.168.10.10 eveseat.test

5. For some odd reason, they suggest installing [Bonjour Print Services](https://support.apple.com/kb/DL999?viewlocale=en_US&locale=en_US). I assume this configures the network or similar?

6. Then you should be able to execute `vagrant up` from your `~/Homestead` directory.
# Homestead Set-up for Windows 10

### Reference Links:
- [EVESeat Documentation - Developer Installation](https://github.com/eveseat/docs/blob/master/docs/developer_guides/developer_installation.md)
- [Laravel Homestead](https://laravel.com/docs/6.x/homestead)
- [Bonjour Print Services](https://support.apple.com/kb/DL999?viewlocale=en_US&locale=en_US)
- [Vagrant](https://www.vagrantup.com/downloads.html)

### Initial Setup:

1. Choose a virtualization provider (VMWare, VirtualBox, Parallels, etc). This guide uses VirtualBox 6. 
2. Install [Vagrant](https://www.vagrantup.com/downloads.html)
   and run the following command: `vagrant box add laravel/homestead`
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

        192.168.10.10 eveseat.test

5. The Homestead documentation recommends installing [Bonjour Print Services](https://support.apple.com/kb/DL999?viewlocale=en_US&locale=en_US). It is unclear as to why this is needed, though if you have issues it's best to install it.

6. Then you should be able to execute `vagrant up` from your `~/Homestead` directory.

### Configuring EVESeat
1. Copy the `.env.example` file, and rename it to `.env`
2. Several settings need to be configured within this environment file:
  - **APP_URL**:     This is the base URL for the entire application, including the authentication callback URL. This value should be set to `http://eveseat.test`
  - **DB_HOST**:     Set to `localhost`. We will configure EVESeat to use the built-in MariaDB instance in the Vagrant box.
  - **DB_DATABASE**:    `homestead`
  - **DB_USERNAME**:    `homestead`
  - **DB_PASSWORD**:    `secret`
  - **QUEUE_CONNECTION**:     `sync`
3. Generate a new application on [developers.eveonline.com/](http://developers.eveonline.com/), with the callback url being 
`EVE_CALLBACK_URL=http://eveseat.test/auth/eve/callback`. Request all scopes for the application, to ensure you don't need to create a new application in the future. Store the ClientID and secret key under the appropriate properties in `.env`

### Extra Notes
- Restarting the vagrant box is as simple as running the following commands:
    ```
    vagrant destroy
    
    vagrant up
    ```

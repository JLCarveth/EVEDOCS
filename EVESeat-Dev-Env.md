# EVESeat Guide: Setting up a 4.0.x Development Environment
*Last Updated 2020-03-11*

---

1. Clone the `eveseat-dev` repository with the following command:

    `git clone http://github.com/icarus-industries/eveseat-dev eveseat`
2. Move into the newly created directory, and initialize the [submodules](https://git-scm.com/book/en/v2/Git-Tools-Submodules):
    
    `git submodule update --init --recursive`
    The submodules are located within the `/packages/eveseat` folder.
3. Each submodule must now be set to pull from the `4.0.x` branch, if it is available for that package. Note that `eseye` does not have a `4.0.x` branch, so it will instead pull from `master`.
    Within each package, run the following commands:

    `git checkout origin/4.0.x`
    `git pull origin 4.0.x`
4. Now, ssh into your Vagrant box. This is done by executing `vagrant ssh` from your Homestead installation folder. `cd` into your `eveseat` folder. Several commands will need to be executed.

    - `composer install` will install all required dependencies for EVESeat to run.
    - `php artisan migrate` will run the database migrations.

5. Finally, ensure the `.env` file has been created, properly configured, and placed within the `eveseat` directory.

You should now be able to navigate to EVESeat via the configured URL.

---

### Some Additional Information

- You may want to grant your character admin rights for the site. To do so, ssh into the vagrant box and run `php artisan seat:admin:login`. This will generate a URL valid for ~60 seconds that will authorize your character.

- If needed, ensure the SDE data is installed with the following command: `php artisan eve:update:sde`

- All available commands can be seen by executing `php artisan` within the vagrant box.
# Setup

Run the following command to create a new Laravel application:
```
curl -s https://laravel.build/new-sail-application | bash
```

Next, navigate into the project directory and run the following command:
```
cd new-sail-application
./vendor/bin/sail up
```

# Adding Sail to an existing application

You can also install Sail in an existing application using Composer:
```
composer require laravel/sail --dev
```

Once the installation is complete, you can publish Sail’s docker-compose.yml file in your project directory using the following command
```
php artisan sail:install
```

Then sail up your project!
```
./vendor/bin/sail up
```

# Alias

In your home directory  there is a file called .*rc, add this code and then you will be able to use the sail command.
```
alias sail='bash vendor/bin/sail'
```

Sail commands:
```
sail up
sail up -d
sail down
```

> When running artisan, composer, and npm commands, the sail alias must precede the commands.

For example instead of running:
```
php artisan migrate
```
You run:
```
sail artisan migrate
```

And instead of running:
```
composer require laravel/sanctum
```
You run:
```
sail composer require laravel/sanctum
```

# Troubleshooting

If you face the following problem after running the command to download Laravel via Sail, you must install/re-install PHP.

> Problem
```
"No configuration file provided: not found"
```

> Solution

```
composer install
```

```
php artisan sail:install 
```

> The solution above failed? Try to uninstall and re-install everything.

Uninstalling Composer

Find where composer is installed with:
```
which composer
```
An example of uninstalling composer at usr/local/bin:
```
cd usr/local/bin
rm -r composer
```
Optional: Deleting the rest of composer files.
```
cd /
cd Users/<hereYourUserName>
rm -r .composer 
```

Uninstalling PHP

Find the version of PHP you are using:
```
php -v
```

An example of uninstalling PHP 8.2:
```
brew uninstall php@8.2
OR
brew uninstall --force php@8.2 
```

Installing PHP and Composer:
```
brew install php
brew install composer
```

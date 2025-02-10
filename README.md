# Setup web development in linux

The official Laravel Valet development environment is great for Apple users, but there is no official Valet for Linux or Windows. However, the community has created two versions of Valet for Linux:

- **[cpriego/valet-linux](https://github.com/cpriego/valet-linux) (Valet Linux)**
- **[genesisweb/valet-linux-plus](https://github.com/genesisweb/valet-linux-plus) (Valet Linux+)**
- **[nvm-sh/nvm](https://github.com/nvm-sh/nvm) (Node Version Manager)**

Among these, **Valet Linux+** has more features, such as MySQL database handling from the command line, MailHog, Redis, sharing sites on LAN, securing sites with TLS (HTTPS), and more.

This guide will show you how to install **Valet Linux+** on an Ubuntu system.

## Requirements

- **Ubuntu or any ubuntu base distro**

## Install Dependencies

```bash
sudo apt-get install network-manager libnss3-tools jq xsel
```

## Install PHP & Extensions

Add the PHP PPA and install PHP 8:

```bash
sudo apt install software-properties-common
sudo add-apt-repository ppa:ondrej/php
sudo apt update
sudo apt install php8.0-fpm
```

Install required PHP extensions:

```bash
sudo apt install php8.0-cli php8.0-common php8.0-curl php8.0-mbstring php8.0-opcache php8.0-readline php8.0-xml php8.0-zip php8.0-mysql php8.0-gd
```

Install other PHP version:

```bash
sudo apt install php<version>-fpm
```

Install required PHP extensions:

```bash
sudo apt install php<version>-cli and other do the same
```

## Install MySQL Server

Valet Linux+ installs MySQL automatically, but it's better to install it manually:

```bash
sudo apt-get -y install mysql-server
```

### Configure MySQL Authentication

```bash
sudo mysql
```

Then, run the following commands in the MySQL shell:

```sql
ALTER USER 'root'@'localhost' IDENTIFIED WITH mysql_native_password BY 'password';
FLUSH PRIVILEGES;
exit;
```

Now, you can log in using:

```bash
mysql -u root -p
```

## Install Composer

Install Composer using `curl`:

```bash
sudo apt install curl
curl -sS https://getcomposer.org/installer | sudo php -- --install-dir=/usr/local/bin --filename=composer
```

Verify installation:

```bash
composer --version
```

## Install Valet Linux+

```bash
composer global require genesisweb/valet-linux-plus
```

Add the following to your shell profile (`~/.bash_profile`, `~/.bashrc`, or `~/.zshrc`):

```bash
export PATH="$PATH:$HOME/.config/composer/vendor/bin"
```

Reload configuration using :

```bash
source ~/.zshrc
```

Restart your terminal and install Valet:

```bash
valet install
```

This installs Valet Linux+, Nginx, MySQL, Redis, Mailhog, and DnsMasq.

## Verify Installation

Run:

```bash
ping -c1 foobar.test
```

## park location

```bash
valet park
```

## link a project

```bash
valet link
```

## show all links

```bash
valet links
```

## secure link

```bash
valet secure
```

## Installing NVM

```bash
curl -o- https://raw.githubusercontent.com/nvm-sh/nvm/v0.37.2/install.sh | bash
```

Attempts to add the source lines from the snippet below to the correct profile file (~/.bash_profile, ~/.zshrc, ~/.profile, or ~/.bashrc).

```bash
export NVM_DIR="$([ -z "${XDG_CONFIG_HOME-}" ] && printf %s "${HOME}/.nvm" || printf %s "${XDG_CONFIG_HOME}/nvm")"
[ -s "$NVM_DIR/nvm.sh" ] && \. "$NVM_DIR/nvm.sh" # This loads nvm
```

Reload configuration using :

```bash
source ~/.zshrc
```
Check the installed version, by running:

```bash
nvm --version
```

See  list all available node.js versions:

```bash
nvm ls-remote

```

Install latest LTS version of node:

```bash
nvm install --lts

```


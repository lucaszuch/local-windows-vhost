# Local Development Env for Windows
How to setup a local development server and vhosts on Windows.

## Requirements: :books:
- Developer access level (requested via support).
- XAMPP (multiple versions recommended).
- HeidiSQL or similar.
- Node.js
- Composer.
- Terminal (Windows Powershell - recommended).
- IDE (VS Code or PHP Storm - both recommended).

## Initial setup: :alembic:
- After having your access level granted, install all the applications. 
- Some of the applications will not be allowed within the C: drive due to access limitations. As an option, install it in your local user.

## XAMPP settings: :alembic:
XAMPP is not going to start as usual, some standard company softwares are using the port 80. As a result, we will need to implement some changes.
- You might need multiple versions to run different site, install xampp identifying on the name which PHP version you are using. E.g. xampp7_1, xampp74, etc.
- On your panel access the Apache configuration (Config button) and select httpd.conf.
- Locate: #Listen 12.34.56.78:80 / Listen 80.
- Replace it with: #Listen 12.34.56.78:8080 / Listen to 8080. If you are using multiple xampp version, set to different ports. E.g. 8081 for 8.0, 8071 for 7.1.
- No changes are needed for MySQL.
- Quit your panel to restart the Apache server. If setting up multiple XAMPP installation, make sure to stop the APACHE service (cmd + r: services.msc) or QUIT the application.
- XAMPP versions > 7.3.x automatically adjust the APACHE files to the correct paths, if you are installing any version older than that, you will need to locate and correct all paths (including SQL, APACHE, and PHP configuration files).

## HeidiSQL settings: :alembic:
HeidiSQL is going to support you in big DB tasks and allow your to access remote servers.
### Setup local server:
-
### Setup remove server:
-

## Setup vhosts: :computer:
Now, we're ready to crack new projects. In order to make our life easier we will setup multiple virtual hosts, that way we can call individual URLs and set config files directly to it.
### XAMPP vhosts:
- Quit XAMPP and stop all the services.
- Navigate to: path\xampp\apache\conf\extra.
- Open the file: httpd-vhosts.conf using notepad.
- At the bottom of the file add the following code:
```
<VirtualHost *:8080>
DocumentRoot "C:/xampp/htdocs"
ServerName localhost
</VirtualHost>

<VirtualHost *:8080>
DocumentRoot "C:/xampp/htdocs/<your-project>/server"
ServerName <desired-url>:8080
</VirtualHost>
```
Note that 8080 has to match the port you have setup.

### Windows vhosts:
- Navegate to: path/Windows/System32/drivers/etc.
- Open the hosts file. You might need to use VSCode as administrator access is required to make changes at this level.
- At the bottom of the file add your necessary vhosts using: 127.0.0.1 <desired-url> (e.g. 127.0.0.1 dlight.loc).
- Save the file.
- You can now access the project via the browser using: http://desired-url:8080 and that's likely the $CFG->wwwroot used on projects.

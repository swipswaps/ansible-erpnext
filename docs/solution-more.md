# More

Each of the following solutions has been proven to be effective and we hope to be helpful to you.


## Domain binding

The precondition for binding a domain is that ERPNext can accessed by domain name.

Nonetheless, from the perspective of server security and subsequent maintenance considerations, the **Domain Binding** step cannot be omitted.

ERPNext domain name binding steps:

1. Connect your Cloud Server
2. Modify [Nginx vhost configuration file](/stack-components.md#nginx), change the **server_name**'s value to your domain name
   ```text
   server
   {
   listen 80;
   server_name name;  # 此处修改为你的域名
   root /data/wwwroot/frappe-bench/sites;
   ...
   }
   ```

## Reset password

There are two main measures to reset password.

### Change password

1. Log in to the background of ERPNext and open Settings > personal settings to find the password modification item
![ERPNext change password](https://libs.websoft9.com/Websoft9/DocsPicture/en/erpnext/erpnext-modifypw-websoft9.png)
2. Set the new password directly and take effect after saving

### Forgot Password

Try to retrieve your password by the following commands when forgot it.

````
sudo -H -u erpnext bash -c "cd /data/wwwroot/frappe-bench && export GIT_PYTHON_REFRESH=quiet && /usr/local/bin/bench set-admin-password newpassword"
````

## Using RDS

If the user does not like to use the MariaDB installed on the server and wants to migrate to the cloud database (RDS), the general process is as follows:

1. Back up the existing database and import it into RDS (suitable for ERPNext has been installed)
2. Edit [database configuration file] (/zh/stack)-components.md#erpnext ）Medium. Add db_host is the external database address
3. Modify the account information
4. Test the connection availability after changing the database

>For more database connection parameters, please refer to the official document [standard config](https://frappeframework.com/docs/user/en/basics/site_config#mandatory-settings)
\\n[mininav_troubleshooting](/home/www/zendstudio/dokuwiki/bin/lib/exe/fetch.php?id=&media=mininav_troubleshooting)

A **Publisher** can reset any user's password. Provided there's at least
one publisher who can log in, ask them to reset your password for you.

### Resetting a password {#resetting-a-password .sectionedit1#resetting_a_password}

If you're the only user with [Publisher
privileges](/home/www/zendstudio/dokuwiki/bin/doku.php?id=user_roles_and_permissions)
(or the only Textpattern user at all), you'll need to access the
database directly to reset your password. Most web hosting accounts
provide direct MySQL access using a program called phpMyAdmin, or via
the command line. If you're not sure how to access either of these, ask
your hosting company's tech support.

There are two main ways to do this.

#### Via the command line {#via_the_command_line}

With phpMyAdmin, or at the MySQL command prompt, run the following
query:

    update txp_users set pass=password(lower('pass')) where name='user';

where

    pass

is the new password, and

    user

is the login username.

#### Via phpMyAdmin {#via_phpmyadmin}

<ol>
<li>
Start phpMyAdmin. This may be done from a shell or your host's control
panel

</li>
<li>
At the opening screen, select the database for your Textpattern install
(e.g. userid_textpattern)

</li>
<li>
From the list of tables select txp_users. This should present a table
structure and a selection of tabbed options

</li>
<li>
Select the **Browse** tab. This will display a query field and a list of
users

</li>
<li>
Click on the small pencil (edit) icon next to the user ID entry you wish
to edit. This will display a table for the record showing the fields and
their current values. Note that only the password hash is displayed, not
the plain text

</li>
<li>
<p>
In the function column for the

</p>
    pass

<p>
field, select PASSWORD from the drop down box. You may then delete the
hash and enter a plaintext password in the corresponding value field.
Letters in this field should be all lowercase. Make sure the box at the
lower left says 'save' and click on the GO button. You will be returned
to the previous screen which will display the SQL query you just
created. The hash displayed opposite the user ID you selected should
have changed (unless you used the exact same password)

</p>
</li>
<li>
Exit phpMyAdmin and login to Textpattern with your username and new
password

</li>
</ol>
### Changing permission level {#changing-permission-level .sectionedit2#changing_permission_level}

It has happened to people before that while learning the nature of
different permission settings they accidentally set themselves at a
lower permissions level than they intended to have; for example as
Managing Editor instead of Publisher.

You can fix this situation, but you have to have access to a database
management program like phpMyAdmin for the database involved. This is
what you do:

1.  Open phpMyAdmin, select the appropriate database, and browse to the
    txp_users table
2.  Look for the row with your Textpattern account username, and find
    the column named “privs”
3.  Change it to the number “1” and save the changes


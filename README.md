# Admin modules (for use in making custom modular input pages in Splunk)

This is a collection of admin modules that are useful for building modular input pages in Splunk.

Splunk doesn't allow multiple admin modules with the same name, thus, this includes a build script which will allow you to make modules with a custom prefix specfically for your app.

# How do I use this?

1) Download and install Ant: https://ant.apache.org/bindownload.cgi
2) Run "ant" from the root directory
3) Include the modules from the package that was created in your app

# Modules included

1) **hide_optional_settings**: Allows you to group options on the input and hide them until the user clicks to open the section
2) **password_copy_fix**: Copies the password from the password entry box to confirmation box (prevents errors that require you to re-enter the password every time you edit an input)
3) **secure_password_storage**: A module that stores the input password in secure storage
4) **selection_dialog**: A module that shows a list and allows people to select an entry from a list
5) **sourcetype_selection_fix**: A module that corrects an issue where the sourcetype is not correctly saved when it is set to auto

## secure_password_storage

This module will make your app use secure storage for the password stored witn the input. This module not save the username in secure storage, you should store this elsewhere (such as in your inputs.conf). The username was not stored in secure storage because doing so:

1) Means you cannot store a username if the password is blanked out. Secure storage doesn't allow an entry with a blank password and thus requires you delete the entire entry (including the username) when you want to clear the password.
2) Secure storage changes the stanza names based on the username. This means changing the username means the password entry is a constantly moving target.

Instead, the username will be hard-coded as "IN_CONF_FILE" (since the username is stored in the conf file).

This module assumes that your input stores the username in a field called "username" and password in a field called "password".


| Parameter           | Purpose                                                                                                                                                                                                                                                                                                                                             | Example      |
| --------------------- | -----------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|-------------- |
| prefix              | Defines the prefix that will appended to the input name. This ought to match the prefix that would be appended to your input in inputs.conf. This parameter is used to set the realm of the secure password entry so as to make it possible to find the password entry for the given input later. The realm is being used as the unique identifier. | web_input:// |
| passwordExampleText | To define the help to the user under the password field (this is optional)                                                                                                                                                                                                                                                                          |              |
| usernameExampleText | To define the help to the user under the username field (this is optional)                                                                                                                                                                                                                                                                          |              |

Below is an example of this module being used (from the Website Input app):

```
<element name="secure_password_storage" type="website_input_secure_password_storage">
    <view name="edit"/>
    <view name="create"/>
    <key name="prefix">web_input://</key>
    <key name="passwordExampleText">The password to use for authenticating (only HTTP authentication supported)</key>
    <key name="usernameExampleText">The username to use for authenticating (only HTTP authentication supported)</key>
</element>
```

Here are some tips if you are converting your app to use secure storage for passwords:

1) You use the helper functions from the [modular_input helper library](https://gist.github.com/LukeMurphey/7479309) to retrieve the password
2) Make sure to update your conf file specs to note that the password field should no longer be used within the conf file
3) If you are saving a password globally via setup.xml, then will likely want to use a SimpleXML setup page to handle the password. See https://github.com/LukeMurphey/splunk-simplexml-setup-example for some guidance. You can use the [SetupView.js](https://gist.github.com/LukeMurphey/a4426a951479a19371aad3dd826ab002) class which includes some utility functions for accessing secure storage.




# Admin modules (for use in making custom modular input pages in Splunk)

This is a collection of admin modules that are useful for building modular input pages in Splunk.

Splunk doesn't allow multiple admin modules with the same name, thus, this includes a build script which will allow you to make modules with a custom prefix specfically for your app.

# Modules included:

1) hide_optional_settings: Allows you to group options on the input and hide them until the user clicks to open the section
2) password_copy_fix: Copies the password from the password entry box to confirmation box (prevents errors that require you to re-enter the password every time you edit an input)
3) secure_password_storage: A module that stores the input password in secure storage
4) selection_dialog: A module that shows a list and allows people to select an entry from a list
5) sourcetype_selection_fix: A module that corrects an issue where the sourcetype is not correctly saved when it is set to auto

# How do I use this?

1) Download and install Ant: https://ant.apache.org/bindownload.cgi
2) Run "ant" from the root directory
3) Include the modules from the package that was created in your app
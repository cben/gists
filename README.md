Gists
=====

CLI interface for managing GitHub gists

Install
-------

Two ways of installation:

* [Download](https://github.com/jdevesa/gists/zipball/master) the source code, extract it, and execute `python setup.py install`
* pip install gists (not yet!)

Configure
---------

First time you run 'gists', execute the command


    $ gists credentials -u your_github_user -s your_github_password


And the file ~/.gistsrc (which stores the 'gists' configuration) will be written
with your GitHub username and its password.

You can live without this config file using the '-u (--user)' argument every
time you perform an action, and '-s (--secret)' argument every time you perform an 
action that needs authentication (create, update, delete gists, and view private gists
as well).

Use it!
-------


### SetUp credentials ###

Gists uses the file '~/.gistsrc' to obtain your GitHub user and password. First thing you need to do is set up your
credentials to perform actions that needs authentication. Method is just:

<!-- language: bash -->
    $ gists credentials -u your_github_user -s your_github_password

You can perform this actions many times you like to override the values.


### List of Gists ###

Return a list of gists. Basic usage is:

<!-- language: bash -->
    $ gists list

That will return a list of Gists from the configured user in your (~/.gistsrc) file. 

More arguments:

* __-u__ (--user) argument you specifies from which user you want to retrieve his/her gists.
* __-p__ (--private) argument retrieves the private gists of the user besides the public ones. (Needs authentication)
* __-s__ (--secret) argument overrides the password from the (~/.gistsrc) file.


### Show a Gist ###

Shows a Gist. There are two modes here: without the __-f__ argument, that will show the Gist metadata (url, description, name of the files...) and with the __-f__ argument, that specifically returns the content of one of the files of the Gist. Identifier of the Gist, (obtained via `gists list`) is mandatory as first argument.

Example without __-f__ argument:

    $ gists show 834ab572ab62064af23c

Example with __-f__ argument:

    $ gists show 834ab572ab62064af23c -f examplegist.py


### Download a Gist ###

Download a file from a Gist using the 'get' action. While in the 'show' action the parameter __-f__ is optional depending on the kind of data you want to show, here is mandatory. So, a basic usage is:

    $ gists get 834ab572ab62064af23c -f examplegist.py

The name of the target file in your OS will be the same of the argument provided by __-f__. There is no way to change this.

More arguments:

* __-o__ (--output\_dir) destination directory where you want to save the gist


### Create a Gist ###

Creates a Gist. Needs a file to be uploaded. So, authentication and __-f__ arguments are required. Basic usage is:

    $ gists create -f file_to_upload.py

The name of the file in the OS will be the same of the name of the file in the Gist. No way to change this.

More arguments:

* __-u__ (--user) Overrides the default user specified in ~/.gistsrc file. This will be the owner of the Gist. If you specify this argument you might need to use the __-s__ as well.
* __-s__ (--secret) Overrides the default password specified in ~/.gistsrc file.
* __-p__ (--private) whenever you want the Gist to be private.
* __-d__ (--description) Set the description of the Gist.
* __-i__ (--input\_dir) Specify the input directory where the file is.


### Update a Gist ###

Update an existent Gist. Several examples:

#### Modify just the description ####

To modify the description, use the __-d__ (--description) argument:

    $ gists update 834ab572ab62064af23c -d "New gist description"

#### Modify the contents of a file ####

Modify the contents of a File that already exists in the Gist:

    $ gists update 834ab572ab62064af23c -f updated_file_content.py

#### Add a new file to a Gist ####

Modify a Gist adding a new file, using the __-n__ (--new) argument:

    $ gists update 834ab572ab62064af23c -f new_file_to_gist.py -n

#### Remove a file from a Gist ####

Modify a Gist removing one of its files, using the __-r__ (--remove) argument:

    $ gists update 834ab572ab62064af23c -f no_longer_needed_file.py -r

#### More arguments ####


* __-u__ (--user) Overrides the default user specified in ~/.gistsrc file. This will be the owner of the Gist. If you specify this argument you might need to use the __-s__ as well.
* __-s__ (--secret) Overrides the default password specified in ~/.gistsrc file.
* __-i__ (--input\_dir) Specify the input directory where the file is.
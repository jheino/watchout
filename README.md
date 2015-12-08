watchout
========

``watchout`` is a Python script which wraps any command and displays its output 
only if it has changed since the last run. It is useful e.g. in monitoring 
systems and sending an e-mail alert if a condition changes.

Typically you will want to use ``watchout`` in a recurring cron job which will 
mail any output to you.

Examples
--------

Print your IP address if it has changed:

	watchout curl -qsS http://icanhazip.com/

Notify if your system has rebooted:

	watchout awk '/btime/ { print "System rebooted at " strftime("%c", $2) }' /proc/stat

Requirements
------------

``watchout`` requires Python 2.7 or 3.2. Other versions might work, but they 
have not been tested.

Implementation
--------------

``watchout`` creates an SQLite database in ``~/.watchout`` where it will store 
an MD5 digest of the command output. A list representation (e.g. ``['curl', 
'-qsS', 'http://icanhazip.com/']``) of all the command line arguments is used as 
the key.

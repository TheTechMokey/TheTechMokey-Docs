Fedora Commands
===============

.. contents::
   :local:
   :depth: 1

Command Structure
-----------------

.. code-block::

    command [-flag(s)] [-option(s) [value]] [argument(s)]

Definitions
------------

**Flags:**
Flags are single-letter options prefixed by a hyphen (`-`). They typically do not require a value and are used to enable or disable features of the command.

**Options:**
Options are more descriptive parameters prefixed by one or two hyphens (`-` or `--`). They usually take a value to modify the behavior of the command.

**Values:**
Values are the data provided to options. They can be arguments, numbers, or text that configure how the command operates.

**Arguments:**
Arguments are inputs to the command, such as filenames, directories, or other data the command will process.

**Examples:**
For the command ``command -f -v value argument``, ``-f`` is a flag, ``-v``` is an option with the value ``value``, and ``argument`` is an argument.

.. _~:

~
~~~
**Description:**

The ``~`` symbol represents the home directory of the current user. It provides a shorthand way to reference files and directories located in this directory.

**Arguments:**

- `~`: Refers to the current user's home directory (e.g., `/home/username`).
- `~username`: Refers to the home directory of a specified user (e.g., `/home/otheruser`).

**Example:**

.. code-block:: bash

   cd ~/Documents          # Changes directory to the Documents folder in the current user's home directory
   ls ~/.config            # Lists files in the .config directory of the current user's home directory
   cp ~/file.txt /tmp/     # Copies file.txt from the current user's home directory to /tmp
   nano ~/.bashrc          # Edits the .bashrc file in the current user's home directory

.. _awk:

awk
~~~~

**Description:**

A powerful text processing tool that allows for pattern scanning and processing.

**Flags and Options:**

- `-F fs`: Specifies the input field separator.
- `-v var=value`: Assigns a value to a variable.
- `-f program-file`: Reads the AWK program source from the file.
- `-W`: Controls optional features (e.g., `-W version`).

**Example:**

.. code-block:: bash

   awk -F: '{ print $1 }' /etc/passwd

.. _cat:

cat
~~~~

**Description:**

Concatenates and displays the contents of files.

**Flags and Options:**

- `-n`: Number all output lines.
- `-b`: Number non-blank output lines.
- `-E`: Display `$` at the end of each line.
- `-T`: Display TAB characters as `^I`.

**Example:**

.. code-block:: bash

   cat -n filename.txt

.. _cd:

cd
~~~~

**Description:**

Changes the current directory.

**Flags and Options:**

- `-P`: Use the physical directory structure without following symbolic links.
- `-L`: Use the logical directory structure with symbolic links.

**Example:**

.. code-block:: bash

   cd /home/user

.. _chmod:

chmod
~~~~~~

**Description:**

Changes the file modes or Access Control Lists (ACLs) of files.

**Flags and Options:**

- `-R`: Change files and directories recursively.
- `-v`: Verbose mode.
- `--reference=RFILE`: Use RFILE’s mode instead of specifying MODE values.
- `-c`: Report only when a change is made.

**Example:**

.. code-block:: bash

   chmod -R 755 /path/to/directory

.. _chown:

chown
~~~~~~

**Description:**

Changes the ownership of files and directories.

**Flags and Options:**

- `-R`: Operates on files and directories recursively.
- `-f`: Suppress most error messages.
- `-v`: Output a diagnostic for every file processed.
- `--from=CURRENT_OWNER:CURRENT_GROUP`: Change the owner only if the current owner is set to CURRENT_OWNER and the current group is set to CURRENT_GROUP.

**Example:**

.. code-block:: bash

   chown -R user:group /path/to/directory

.. _cp:

cp
~~~

**Description:**

Copies files and directories.

**Flags and Options:**

- `-r`: Copy directories recursively.
- `-a`: Archive mode (preserves attributes and follows symbolic links).
- `-v`: Verbose mode, showing files being copied.
- `-u`: Copy only when the source file is newer or when the destination file is missing.

**Example:**

.. code-block:: bash

   cp -r /source/directory /destination/directory

.. _curl:

curl
~~~~~

**Description:**

Transfers data from or to a server using various protocols.

**Flags and Options:**

- `-O`: Save the file with the remote file name.
- `-L`: Follow redirects.
- `-d`: Send specified data in a POST request.
- `-H`: Pass custom header(s) to the server.
- `-u`: Use username and password for server authentication.

**Example:**

.. code-block:: bash

   curl -O http://example.com/file.txt

.. _df:

df
~~~

**Description:**

Displays disk space usage of file systems.

**Flags and Options:**

- `-h`: Human-readable format.
- `-T`: Display file system type.
- `-i`: Display inode information.
- `-P`: Display output in POSIX format.

**Example:**

.. code-block:: bash

   df -h /

.. _diff:

diff
~~~~~

**Description:**

Compares files line by line.

**Flags and Options:**

- `-u`: Unified format.
- `-c`: Context format.
- `-i`: Ignore case differences.
- `-r`: Recursively compare directories.
- `-q`: Report only when files differ.

**Example:**

.. code-block:: bash

   diff -u file1.txt file2.txt

.. _du:

du
~~~

**Description:**

Estimates file space usage.

**Flags and Options:**

- `-h`: Human-readable format.
- `-s`: Display only the total size.
- `-a`: Display sizes of all files.
- `-c`: Produce a grand total.
- `-d`: Display a specific number of directory levels.

**Example:**

.. code-block:: bash

   du -sh /path/to/directory

.. _echo:

echo
~~~~~

**Description:**

Displays a line of text or a variable value.

**Flags and Options:**

- `-n`: Do not output the trailing newline.
- `-e`: Enable interpretation of backslash escapes.

**Example:**

.. code-block:: bash

   echo "Hello, World!"

.. _find:

find
~~~~~

**Description:**

Searches for files in a directory hierarchy.

**Flags and Options:**

- `-name`: Search by file name.
- `-type`: Search by file type (e.g., `f` for file, `d` for directory).
- `-exec`: Execute a command on the found files.
- `-mtime`: Search by modification time.
- `-size`: Search by file size.

**Example:**

.. code-block:: bash

   find /path -name "*.txt"

.. _grep:

grep
~~~~~

**Description:**

Searches for patterns within files.

**Flags and Options:**

- `-i`: Ignore case.
- `-r`: Recursively search directories.
- `-v`: Invert the match (return non-matching lines).
- `-l`: Display only the names of matching files.
- `-n`: Display the line number of matching lines.

**Example:**

.. code-block:: bash

   grep -i "search_term" file.txt

.. _head:

head
~~~~~

**Description:**

Outputs the first part of files.

**Flags and Options:**

- `-n`: Number of lines to display.
- `-c`: Number of bytes to display.
- `-q`: Suppress header lines when displaying multiple files.

**Example:**

.. code-block:: bash

   head -n 10 file.txt

.. _history:

history
~~~~~~~~

**Description:**

Displays or manipulates the command history.

**Flags and Options:**

- `-c`: Clears the history list.
- `-d offset`: Deletes the history entry at the specified offset.
- `-a`: Appends the new history entries to the history file.
- `-w`: Writes the current history to the history file.
- `-r`: Reads the history file and appends the entries to the history list.

**Example:**

.. code-block:: bash

   history | grep "search_term"

.. _kill:

kill
~~~~~

**Description:**

Sends a signal to a process.

**Flags and Options:**

- `-9`: Sends the SIGKILL signal (forceful termination).
- `-l`: Lists all signal names.
- `-s signal`: Specifies the signal to send.
- `-p`: Specify process IDs directly.

**Example:**

.. code-block:: bash

   kill -9 1234

.. _less:

less
~~~~~

**Description:**

Views file contents one screen at a time.

**Flags and Options:**

- `-N`: Display line numbers.
- `-S`: Chop long lines instead of wrapping them.
- `-G`: Suppress the message about the end of file.
- `-F`: Exit if the entire file can be displayed in one screen.

**Example:**

.. code-block:: bash

   less file.txt

.. _ls:

ls
~~~

**Description:**

Lists directory contents.

**Flags and Options:**

- `-l`: Long listing format.
- `-a`: Include hidden files.
- `-h`: Human-readable file sizes.
- `-R`: List directories recursively.
- `-t`: Sort by modification time.

**Example:**

.. code-block:: bash

   ls -la /path

.. _man:

man
~~~~~

**Description:**

Displays the manual page for a command.

**Flags and Options:**

- `-k keyword`: Search for a keyword in the manual page database.
- `-f command`: Display a brief description of the command.
- `-a`: Display all pages for the command.

**Example:**

.. code-block:: bash

   man ls

.. _mkdir:

mkdir
~~~~~~~

**Description:**

Creates directories.

**Flags and Options:**

- `-p`: Create parent directories as needed.
- `-m mode`: Set the permissions for the directory.

**Example:**

.. code-block:: bash

   mkdir -p /path/to/directory

.. _mv:

mv
~~~

**Description:**

Moves or renames files and directories.

**Flags and Options:**

- `-i`: Prompt before overwrite.
- `-u`: Move only when the source file is newer.
- `-v`: Verbose mode.

**Example:**

.. code-block:: bash

   mv oldfile.txt newfile.txt

.. _nano:

nano
~~~~~~

**Description:**

A simple text editor.

**Flags and Options:**

- `-c`: Display the current cursor position.
- `-m`: Show mouse support.
- `-w`: Disable wrapping of long lines.

**Example:**

.. code-block:: bash

   nano file.txt

.. _ping:

ping
~~~~~~

**Description:**

Sends ICMP ECHO_REQUEST packets to network hosts.

**Flags and Options:**

- `-c count`: Stop after sending count ECHO_REQUEST packets.
- `-i interval`: Wait interval seconds between sending each packet.
- `-t ttl`: Set the IP Time To Live.

**Example:**

.. code-block:: bash

   ping -c 4 example.com

.. _ps:

ps
~~~

**Description:**

Reports a snapshot of current processes.

**Flags and Options:**

- `-e`: Show all processes.
- `-f`: Display full format listing.
- `-u user`: Display processes for a specified user.
- `-aux`: Show processes for all users.

**Example:**

.. code-block:: bash

   ps -aux

.. _rm:

rm
~~~

**Description:**

Removes files or directories.

**Flags and Options:**

- `-r`: Remove directories and their contents recursively.
- `-f`: Force removal of files without prompting.
- `-i`: Prompt before every removal.

**Example:**

.. code-block:: bash

   rm -rf /path/to/directory

.. _sed:

sed
~~~~~

**Description:**

Stream editor for filtering and transforming text.

**Flags and Options:**

- `-e script`: Specify a script to be executed.
- `-i[SUFFIX]`: Edit files in place (with optional backup suffix).
- `-n`: Suppress automatic printing of pattern space.

**Example:**

.. code-block:: bash

   sed -i 's/old/new/g' file.txt

.. _sort:

sort
~~~~~

**Description:**

Sorts lines of text files.

**Flags and Options:**

- `-n`: Compare according to numerical value.
- `-r`: Reverse the result of comparisons.
- `-k FIELD`: Sort by the specified field.
- `-u`: Suppress duplicate lines.

**Example:**

.. code-block:: bash

   sort -n file.txt

.. _tail:

tail
~~~~~

**Description:**

Outputs the last part of files.

**Flags and Options:**

- `-n`: Number of lines to display from the end of the file.
- `-f`: Follow the end of the file as it grows.
- `-c`: Number of bytes to display from the end of the file.

**Example:**

.. code-block:: bash

   tail -f /var/log/syslog

.. _tar:

tar
~~~~~

**Description:**

Archives files.

**Flags and Options:**

- `-c`: Create a new archive.
- `-x`: Extract files from an archive.
- `-f file`: Use the archive file specified.
- `-v`: Verbose mode.
- `-z`: Compress the archive using gzip.

**Example:**

.. code-block:: bash

   tar -cvzf archive.tar.gz /path/to/directory

.. _top:

top
~~~

**Description:**

Displays real-time system information and processes.

**Flags and Options:**

- `-d delay`: Set the delay between updates.
- `-n number`: Number of iterations before exiting.
- `-b`: Batch mode operation.

**Example:**

.. code-block:: bash

   top -d 5

.. _touch:

touch
~~~~~~~

**Description:**

Changes file timestamps or creates empty files.

**Flags and Options:**

- `-a`: Change the access time only.
- `-m`: Change the modification time only.
- `-t`: Use the specified timestamp.

**Example:**

.. code-block:: bash

   touch file.txt

.. _wget:

wget
~~~~~

**Description:**

Non-interactive network downloader.

**Flags and Options:**

- `-O file`: Save the downloaded content to the specified file.
- `-r`: Download files recursively.
- `-p`: Download all necessary files for displaying HTML pages.

**Example:**

.. code-block:: bash

   wget -O output.html http://example.com

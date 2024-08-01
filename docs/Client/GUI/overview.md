# Overview

This section will provide an overview of the graphical user interface (GUI) Client that users can opt to use instead of the command line interface.

The GUI was developed in Python 3.11, using CustomTkinter (CTk), the UI-library made by Tom Schimansky, as well as Tkinter, the standard Python interface to the Tk GUI toolkit.

When handler_gui.py is first run, users will be greeted by the server connect and login window, which is a separate CTk main loop from the main application. This is done by running login.py, where this window is initialised, in a subprocess using the subprocess module.

Users will first be prompted to connect to the server. Once connected, the window will hide the frame containing the inputs for server connection, and make the frame containing the inputs for user login visible. If the user has successfully logged on before, the username section will be filled in from info.txt.

A window containing the Bamboo logo and a line of trivia will then appear before destroying itself after 2.5 seconds. Similar to the previous window, this is also a separate CTk main loop from the main application, and is run in a subprocess with the subprocess module. Once this window is destroyed, the main application will appear.

The following section will explain more about the main application, as well as the individual widgets.
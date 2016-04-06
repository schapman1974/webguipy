#WebGuiPy

This project is a GUI framework that allows a programmer to code a complete 'GUI' application directly for a web browser by using only Python Code.  The framework has its own function calls that will directly send commands to the ajax portion of this system and communicate with the widgetset library to accomplish a 'GUI' look and feel to the created program.  The widgetset used in this system is provided by dhtmlx.com and is licensed under GPLv2.
    
##Other Components
Other components have been included in this system including the ace editor released under the BSD license.  Other javascript libraries can be added to this project and function calls created for them.

##Single Process WSGI
This system relies heavily on in-memory wsgi sessions to be maintained and should be run as a single process or a single process multiple times with some sort of sticky sessions included implemented for the front end to allow the user to connect to the same process.
    
##Environments
As well this system is designed to run on linux and a windows environment.  And will include binaries for windows use directly as a service.
    
  

#License
GPLv2 
http://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html

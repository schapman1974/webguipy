#WebGuiPy

This project is a GUI framework that allows a programmer to code a complete 'GUI' application directly for a web browser by using only Python Code.  The framework has its own function calls that will directly send commands to the ajax portion of this system and communicate with the widgetset library to accomplish a 'GUI' look and feel to the created program.  The widgetset used in this system is provided by dhtmlx.com and is licensed under GPLv2.
    
###Other Components
Other components have been included in this system including the ace editor released under the BSD license.  Other javascript libraries can be added to this project and function calls created for them.

###Single Process WSGI
This system relies heavily on in-memory wsgi sessions to be maintained and should be run as a single process or a single process multiple times with some sort of sticky sessions implemented for the webserver/proxy to allow the user to connect to the same process. With wsgi threading turned on I have had no problem being able to maintain a high level of availablity on this service.

####Why Single Process
There are three reasons I chose this route for this project.  The first being that the connection objects are very important to the overall experience of being able to just code along in python as if you were writing any other gui program.  The second reason is a bit more in depth but to make it simple the two way communications between python and the browser is easier accomplished if one process is handling it.  Its a bit more in depth than that and there are other ways of dealing with this possibly in the future.  The third reason is a bit more pragmatic.   We are writing gui applications here not web pages so the hit count for what we are building should be no where near a standard web page.  Threading on the wsgi process should still allow an acceptable level of performance.
    
###Environments
As well this system is designed to run on linux and a windows environment.  And will include binaries for windows use directly as a service.
    
###Development Environment
Included in this release is an IDE of sorts that was written using the framework itself.   This IDE will allow for simple modification and previewing of your application.

###Example Code
```python
from rempbapiweb import spool, tr

class module(spool):

    def initScreen(self):
        #Add a menubar to the main window
        self.addMenu("someMenu")
        
        #add a file menu item with save under it
        self.someMenu.addMenuItem("MAIN","file", "File", "WINDOWS.png")
        self.someMenu.addMenuItem("file","save", "Save", "SAVE.png")
        #add an edit menu item with cut/copy/paste under it
        self.someMenu.addMenuItem("MAIN","edit", "Edit", "EDIT.png")
        self.someMenu.addMenuItem("edit","cut",  "Cut",  "CUT.png")
        self.someMenu.addMenuItem("edit","copy", "Copy", "COPY.png")
        self.someMenu.addMenuItem("edit","paste","Paste","PASTE.png")
        
        #Add a toolbar to the main window with 48 point size icons and aligned left
        self.addToolbar("someToolbar",48,"left")
        self.someToolbar.addButton("openfile","Open File","OPENFILE.png")
        self.someToolbar.addStretch()
        self.someToolbar.addButton("exit","Exit","EXIT.png")
        
        #Add the initial Layout to the form and tell the layout what pattern to take
        self.addLayout("demolayout","2E")
        self.demolayout.addGrid("someGrid","a")
        #function fillGrid created below
        self.fillGrid()
        
        #Set the height of element a in the demolayout which is the bottom most layout
        self.demolayout.setHeight(50,"b")
        
        #Add a toolbar to the bottom most layout 32 point size icons and aligned right
        self.demolayout.addToolbar("bottomTool",32,"right","b")
        #Add refresh button to the bottom toolbar
        self.bottomTool.addButton("refresh","Refresh","REFRESH.png")
        
        #add signals
        #add the onClick signalto the menubar and connect it to a function
        self.addSignal(self.someMenu,        "onClick",          self.doMenuBar)   
        # onClick will return the itemname,ischecked,parentname as parameters
        
        #add the onClick signal to the toolbars and connect it to a function.
        self.addSignal(self.someToolbar,     "onClick",          self.doToolBar)
        self.addSignal(self.bottomTool,      "onClick",          self.doToolBar)   
        # onClick will return the button name as a parameter
        
        #add the onRowDblClicked signal to the grid and connect it to a function
        self.addSignal(self.someGrid,        "onRowDblClicked",  self.gridClicked)
        # onRowDblClicked will return rowKey,columnIndex,rowIndex as parameters
        
    def doMenuBar(self,moduleName,isChecked,parentObject):
        self.messageBox("popup",moduleName)
        
    def doToolBar(self,moduleName):
        self.messageBox("popup",moduleName)
        
    def fillGrid(self):
        self.someGrid.clearItems()
        showDat=[['key1','Some Question 1','Some Answer 1','SomeText 1','MoreText 1'],
                 ['key2','Some Question 2','Some Answer 2','SomeText 2','MoreText 2'],
                 ['key3','Some Question 3','Some Answer 3','SomeText 3','MoreText 3'],
                 ['key4','Some Question 4','Some Answer 4','SomeText 4','MoreText 4'],
                 ['key5','Some Question 5','Some Answer 5','SomeText 5','MoreText 5']]
                 
        self.someGrid.setTableHeaders(['Question','Answer','SomeText',"MoreText"])
        self.someGrid.setTableWidths([300,300,300,"*"])
        self.someGrid.setTableColTypes(["ro","ro","ro","ro"])
        self.someGrid.fillTableMany(showDat)
        
    def gridClicked(self,rowKey,columnIndex,rowIndex):
        self.messageBox("popup",rowKey)
```

The code above will render the following screen on the browser.

![Example](https://github.com/schapman1974/webguipy/blob/master/img/webguipyex1.png "Example")
[![Example](https://img.youtube.com/vi/bI3DVL6oyjY/0.jpg)](https://www.youtube.com/watch?v=bI3DVL6oyjY)

#License
GPLv2 
http://www.gnu.org/licenses/old-licenses/gpl-2.0.en.html

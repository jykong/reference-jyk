* You can type ? after starting the console. This will display help about Jupyter. You can exit by typing q.
* You can type %quickref. This is a magic that will tell you some useful commands. We'll talk more about Jupyter magics shortly.
* If you want information about a variable, just type the name of the variable, followed by ?. For information on the dq variable, you'd type dq?.
* Type help() to get access to Python help. This will enable you to get help on all the modules and functions currently available. You can quit by typing quit.
* If you want to use the Python help system to get information on a variable, type help(variable_name). If you wanted help with the variable dq, you'd type help(dq).



* %run -- allows you to run an external Python script. Any variables in the script will be stored in the current kernel session.
* %edit -- opens a file editor. Any code you type into the editor will be executed by Jupyter when you exit the editor.
* %debug -- if there's an error in any of your code, running %debug afterwards will open an interactive debugger you can use to trace the error.
* %history -- shows you the last few commands you ran.
* %save -- saves the last few commands you ran to a file.
* %who -- print all the variables in the session.
* %reset -- resets the session, and removes all stored variables.

Normal Bash Shell Commands `!ls`

* %cpaste -- opens a special editing area where you can paste in code normally, without whitespace being a problem. You can type -- alone on a line to exit. After you exit, any code you pasted in will be immediately executed.
* %paste -- takes code from your clipboard and runs it in Jupyter. This doesn't work on remote systems, where Jupyter doesn't have access to your clipboard.

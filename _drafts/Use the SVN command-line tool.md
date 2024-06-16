

本文转自：<http://www.codeweblog.com/use-the-svn-command-line-tool/>
排版有修改


From <http://subversion.tigris.org> for subversion for windows version, after installation there will be a `svn.exe` the command-line client based tool. Of course, there are also server-side program, here is not concerned about how to configure the SVN service. Setup the path to `svn.exe` joined the path environment variable, we are able to directly enter the svn command line can be used.
If you do not know how to use the command svn command can query as follows: 
`svn help`
That the sub-command, but do not know subcommands can also search for: 
`svn help ci`

## Developers frequently used commands
Import items 
`svn import http://svn.chinasvn.com:82/pthread - message "Start project"`
Export Project 
`svn checkout http://svn.chinasvn.com:82/pthread`
Export to export by way of a "clean" project 
`svn export http://svn.chinasvn.com:82/pthread pthread`
Clearance for the failure of the transaction 
`svn cleanup`
Code changes locally, check the status changes
```
svn status-v
svn diff
```
Update (update) server data to local
```
svn update directory 
svn update file
```
Increase (add) local data to the server
```
svn add file.c 
svn add dir
```
Rename the file and delete
```
svn mv bc bb.c 
svn rm dc
```
Submit (commit) local document to the server
```
svn commit 
svn ci 
svn ci-m "commit"
```
View Log
```
svn log directory 
svn log file
```

## Some related things: 
1, in the local paper, each directory has a. Svn folder (attribute is hidden), save the relevant information. 
2, registered environmental variables SVN_EDITOR as `"E: \ Program Files \ Vim \ vim71 \ gvim.exe"`, results in the svn ci, when an error:
```
'E: \ Program' is not an internal or external command, operable program or batch file.
svn: Commit failed (details follow): 
svn: system ('E: \ Program Files \ Vim \ vim71 \ gvim.exe svn-commit.tmp') returns 1
```
The SVN_EDITOR to "gvim.exe", and add the path in the path `"E: \ Program Files \ Vim \ vim71 \"`, so that you can use vim at the time of submission of written comments.
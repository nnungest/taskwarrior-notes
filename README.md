# My current setup and workflow

Dependencies:
Homebrew: `/usr/bin/ruby -e "$(curl -fsSL https://raw.githubusercontent.com/Homebrew/install/master/install)"`  
Coreutils: `brew install coreutils`


Install taskwarrior 

`brew install task`

Install timewarrior 

`brew install timewarrior` 

Test taskwarrior:
```bash 
task add "example"
task list
task <number> done
```

Now that you have done that, get yourself a custom report for morning standup. 
Lets backup the config file first. 
`cp ~/.taskrc ~/.taskrc.bak`
Then using your favorite editor paste these lines in at the bottom of your ~/.taskrc file: 
```
report.scrum.description=Scrum report for standup
report.scrum.columns=id,uuid.short,project,modified.formatted,description.combined
report.scrum.labels=ID,UUID,Project,Modded,Details
```
*OSX users can copy the above and use `pbpaste >> ~/.taskrc`* 

Cool you can test that out with:

`task scrum modified:today`

Now we don't want to have to type all that out. so lets make this easier. 

In your favorite editor, add these lines to your ~/.bash\_profile.If that file doesnt exist, you can use mine [here](https://github.com/nnungest/.files/blob/master/osx_bashp_boiler.txt "bash_profile"). 

```bash 
#----------------
# scrum meeting setup
#-----------------
alias scrum="task scrum modified:yesterday"
alias tfriday="task scrum modified:$(gdate --date="last friday" +%Y-%m-%d)"
alias ttoday="task scrum modified:today"
```
You'll need to re-source your ~/.bash\_profile after that with: `source ~/.bash_profile`

Once this is all done, you can just run `scrum` from the command line which shows all tasks that were modified the day before. You'll have to stay ontop of closing out tasks to keep this thing working. But it will be easier to keep track of what you've been doing. As you can see from the above `tfriday` runs a report for the previous friday. Note that gdate is used here. You must have coreutils installed `brew install coreutils` for this to work. 

Shoo.. that was alot but now we are somewhat in a better situation to track activities. 

TODO: get timew hook install process documented for taskwarrior. 

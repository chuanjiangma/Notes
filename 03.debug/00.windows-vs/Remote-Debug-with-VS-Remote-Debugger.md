# Remote Debug with VS Remote Debugger

[toc]

## Preparations

Referring to [official document](https://docs.microsoft.com/en-us/visualstudio/debugger/remote-debugging?view=vs-2019), download the remote debug tool and install it to the target remote machine. On the first time start remote debugger, it will ask for configurations, just follow the document.

## Setup the way to look up symbols

Defaultly, visual studio will look up symbols local, which will perform better. But still support configure to look up symbols on remote machine. Actually it is very simple, just keep a same .pdb file on local machine, and set the symbols look up directory in the debug->symbols config panel of the solution.

## Reference

- [Remote debug setting from official site](https://docs.microsoft.com/en-us/visualstudio/debugger/remote-debugging?view=vs-2019)

- may help and waite to confirm: [solve symbols not found and breaks not hit local](https://stackoverflow.com/questions/151966/why-are-no-symbols-loaded-when-remote-debugging)
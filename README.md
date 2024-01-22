# Create a sha256 list 

The goal of this script is to calculate the sha256 of all the files that are stored into the **./files_to_check** subfolder.

Why do we have to do that ?... The answer is : for querying Cisco Talos for file reputations thru XDR APIs.

And we can achieve this either thanks to a dedicated script like the script shared here : 

[check Observables dispositions in CTR from an observable list](https://github.com/pcardotatgit/check_observable_dispositions_in_CTR_from_an_observable_list) 

Or thanks the **XDR Ribbon plugin**. And this is the reason why the output of this script is an HTML file ( index.html ). This is to be able to open the HTML result just by clicking on it and then invoke the XDR plugin within the browser in order to know which files are known as malicious..

A typical use case would be the following. Let's imagine that you browse the INTERNET in order to find a document or a nice freeware that do something you qbsolutely need. Then instead of downloading the tool and run it, what you can do is to download it first into a temporary folder ( into a temporary sandbox ) and then run the script in order to ask to TALOS if the files contained into the folder are known as malicious or not.

A perfect host to use for downloading the files and check their reputation thanks to the script is a raspberry pi. No risk to harm the raspberry pi ( and this is not a problem if it happens ) 

The shared script does the half of the job actually.

The role of the current script is to calculate the sha256 footprints of every files contained into the **./files_to_check** subfolder. 

This script outputs a resulting file named **index.html** which contain file names and their sha256s. 

## how to use this ?


Into the sandbox server ( or into your machine ) create a folder named **check_file_reputation** and copy the python script into it.

In this **check_file_reputation** folder create a subdirectory named **files_to_check**.

The goal is to store all the binaries you could download from the Internet into this subfolder.

Don't hesistate to modify the script in order to point to the endpoint default **download** folder.

Then run the **1-create_a_sha256_list.py** script.

This one will create a resulting file that is an html file named **index.html** in the current directory

Finally the script runs a web server that listen on port 8888.

Then, you can either from your laptop open the **index.html** file, Or from another endpoint launch a browser and open **http://your_sandbox_ip:8888**

Then you will see the sha256 list in the page and you can start the Browser's XDR Ribbon plugin and the mailicious files will appear after a few seconds.

EXPLANATIOIN OF THE SIGNIFICANCE OF THESE FILES



PORTMAN FILES AND EXCEL FILE


These files were created by the portman application (for monitoring serial port communications). 
They were gathered in order to attemp to debug our inability to communicate with the LiCor LI-7000 
device using LabVIEW. Serial communications between the VI's were compared to those obatined from 
the LI-7000 software in hopes of determining what the difference might be between the communication sets.

At this point, we have determined what the issues were (at least roughly speaking - we now have a working 
VI set for communications with this device: the LiCor_init along with the LiCor_poller and the 
LiCor_setting_manager). Storage is cheap, it may be worth keeping these files around for posterity.




THOUGHTS ON THE ISSUES WE WERE HAVING

For data polling, the LiCor instrument seems to fill the buffer with a stack of messages. The 
first two are just line feeds and statuses regarding the correctness of command syntax, so we toss 
these out. The last is the one we care about, the actual data. For setting parameters though, the 
instrument only returns two messages. 

I just realized that it may be breaking the messages up due to the fact that in configuration I have 
it set so that reading stops when a termination character is recieved. It might be worth undoing this 
so that we don't have to put these two empty reads in, particularly if there end up being issues with 
filling up the buffer when there are

Sorry for posting this as flow of thought, but if anyone is digging down this deep it may be useful. 
I just went into Advanced serial Write and Read and played around with some of the settings (ASRL End 
In, Supress End Enable, TermChar Enable and possible one or two others). Through some combination (which 
I think may have been accidental and I have not been able to reproduce though I haven't tried very 
hard - there may have been another setting I played with as well) I was able to get it to return both 
of the messages together (from a (Display(BackLt 1)) command), but I also got a timeout error from this. 
Trying to reset these values to ones that would make shut off the read termination, I was unable to 
reproduce the error, or get the read termination to end. Anyway, this isn't that important - I have 
things working. I just mention this in case someone has troubles down the road and needs to shoot them. 
It's also something of a matter of simple curiosity regarding what was causing the issues before. Nuff said... 






Christopher Small
ThoughtNode Software
Jan 2011
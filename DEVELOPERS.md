

## Handy trick to keep ssh happy ##

````
Host 192.168.0.*
   StrictHostKeyChecking no
   UserKnownHostsFile=/dev/null
````

## All packages in size order ##
````
dpkg-query -W --showformat='${Installed-Size;10}\t${Package}\n' | sort -k1,1n
````
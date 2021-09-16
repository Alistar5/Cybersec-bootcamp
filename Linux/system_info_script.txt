#/bin/bash

free -h >> ~/backups/freemem/free_mem.txt
du -h >> ~/backups/openlist/open_list.txt
lsof >> ~/backups/openlist/open_list.txt

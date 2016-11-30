### Some useful shell commands and functions

#### find

    find <path> -name "bla bla*"        # find files and directories starting with bla bla in <path>
    find <path> -iname "bla bla*"       # i options is case UNsensitive
    find <path> -type f "bla"           # find only files
    find <path> -type d "bla"           # find only directories

#### du

    du -h -d <N> <path>                 # size on disk of everything within depth <N> in <path>
    du -h --summarize <path>            # size on disk of <path> (directory or file)
    du -h -d 0 <path>                   # same as above
    du -h --total <path>                # add a total at the end

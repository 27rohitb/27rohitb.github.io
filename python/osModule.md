
### Returns a list of all the function available in given "module"
### NOTE: this is INDEPENDENT of OS module!!!!
dir(<module_name>)


### Checks if given path exists or not (can be folder or file)
os.path.exists(<_path_>)


### Given Current Working Directory
os.getcwd()


### Change directory to given path
os.chdir(<Absolute_file_path>)


### Return a list all files & folder in the given dir
os.listdir(<optional_absolute_path>)


### Creates a new dir with given name at given path
### NOTE: it is NOT mkdir, because that has limitation of creating dir upto 1-level only.
os.mkdirs(<optional_abs path + dir_name>)


### Remove given directory upto 1-level
### NOTE: it is NOT same as os.removedirs(), which can remove at multiple level, which is dangerous
os.rmdir(<dir_name>)


### Rename file/folder
os.rename(<old_name> , <new_name>)


### Gives data about file- creation time, size etc
os.stat(<file_name>)


### Return a generator that gives a tuple (dir_path, dirs_within_dir, file_within_dir)
### can be used as a local search engine
os.walk(<optional-abs-path +dir_name>)


### Returns the value for "env_name"
### to view all env_vars remove ".get()"
os.environ.get(<env_name>)


### Hassel free join any two paths
os.path.join(<path_1> , <path_2>)

### Return file name at the end
os.path.basename(<_path_>)


### Returns path upto the given file
os.path.dirname(<_path_>)


### Gives a tuple (<abs_path + filename> , <file_extension only>)
os.path.splitext(<_path_>)
